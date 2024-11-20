
# Step 1: Import necessary libraries
import pandas as pd
import numpy as np
from sklearn.preprocessing import MinMaxScaler
import tensorflow as tf
from tensorflow.keras import Sequential
from tensorflow.keras.layers import Dense
import matplotlib.pyplot as plt

# Step 2: Create a sample dataset
data = {
    "SquareFootage": [1500, 1800, 2400, 3000, 3500],
    "Bedrooms": [3, 4, 3, 5, 4],
    "Age": [10, 5, 20, 15, 8],
    "Price": [300000, 400000, 350000, 500000, 450000]
}
df = pd.DataFrame(data)  # Convert dictionary to a DataFrame

# Step 3: Split data into features (X) and target (y)
X = df[["SquareFootage", "Bedrooms", "Age"]].values
y = df["Price"].values

# Step 4: Normalize the data
scaler_X = MinMaxScaler()
scaler_y = MinMaxScaler()
X_normalized = scaler_X.fit_transform(X)
y_normalized = scaler_y.fit_transform(y.reshape(-1, 1))

# Step 5: Define the TensorFlow model
model = Sequential([
Dense(64, activation="relu", input_shape=(3,)),
    Dense(32, activation="relu"),
    Dense(1)
])
model.compile(optimizer="adam", loss="mse", metrics=["mae"])

# Step 6: Train the model
history = model.fit(X_normalized, y_normalized, epochs=100, batch_size=2, verbose=1)

# Step 7: Evaluate the model
loss, mae = model.evaluate(X_normalized, y_normalized, verbose=0)
print(f"Mean Absolute Error: {mae}")

# Step 8: Make predictions
new_house = np.array([[2500, 4, 10]])
new_house_normalized = scaler_X.transform(new_house)
predicted_price_normalized = model.predict(new_house_normalized)
predicted_price = scaler_y.inverse_transform(predicted_price_normalized)
print(f"Predicted Price: {predicted_price[0][0]:.2f}")

# Step 9: Visualize training loss
plt.plot(history.history['loss'])
plt.title('Model Loss')
plt.xlabel('Epochs')
plt.ylabel('Loss')
plt.show()
