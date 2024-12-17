# restaurant-simulation

Creating a simple restaurant simulation game in Unity involves several components, such as managing customers, orders, cooking, and serving food. Below, I'll provide a basic structure for a Unity script to get you started. This example will cover the essentials: a customer, an order system, and a simple UI to display orders.

### Unity Setup
##### 1. Create a new project in Unity.
##### 2. Set up your scene with a Canvas for UI elements (like buttons and text).
##### 3. Create prefabs for customers and food items.

### Basic Game Logic
Here’s a basic example of how you might structure your code. This will include:

- A Customer class
- An Order class
- A RestaurantManager class to handle the flow of the game

### Customer.cs
```
using UnityEngine;

public class Customer : MonoBehaviour
{
    public string customerName;
    public string order;

    public Customer(string name, string order)
    {
        this.customerName = name;
        this.order = order;
    }
}
```
Order.cs
```
using UnityEngine;

[System.Serializable]
public class Order
{
    public string foodItem;

    public Order(string foodItem)
    {
        this.foodItem = foodItem;
    }
}
```
RestaurantManager.cs
```
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class RestaurantManager : MonoBehaviour
{
    public Text orderText;
    public Button serveButton;
    private List<Customer> customers;
    private Queue<Order> ordersQueue;

    void Start()
    {
        customers = new List<Customer>();
        ordersQueue = new Queue<Order>();

        // Example customers
        AddCustomer("Alice", "Burger");
        AddCustomer("Bob", "Pizza");

        UpdateOrderText();
        serveButton.onClick.AddListener(ServeOrder);
    }

    void AddCustomer(string name, string order)
    {
        Customer customer = new Customer(name, order);
        customers.Add(customer);
        ordersQueue.Enqueue(new Order(order));
    }

    void UpdateOrderText()
    {
        orderText.text = "Current Orders:\n";
        foreach (var order in ordersQueue)
        {
            orderText.text += order.foodItem + "\n";
        }
    }

    void ServeOrder()
    {
        if (ordersQueue.Count > 0)
        {
            Order servedOrder = ordersQueue.Dequeue();
            Debug.Log($"Served: {servedOrder.foodItem}");
            UpdateOrderText();
        }
        else
        {
            Debug.Log("No more orders to serve!");
        }
    }
}
```
### Unity Editor Setup

#### 1. <B>Create a UI Canvas</B>:
- Add a <B>Text</B> element for displaying current orders.
- Add a <B>Button</B> for serving the order.
#### <B>Attach Scripts</B>:
- Create an empty GameObject named GameManager.
- Attach the RestaurantManager script to it.
- Assign the Text and Button components to the corresponding fields in the RestaurantManager script via the Inspector.
### Running the Game
Play the game in the Unity editor. You should see the current orders displayed, and clicking the "Serve" button will remove the top order from the list and log it to the console.

### Enhancements
This is a very basic structure. Here are some ways to expand it:

- Add more food items and customize orders.
- Implement a customer satisfaction system based on wait time.
- Create a cooking mini-game when preparing food.
- Add animations for customers and food serving.
- Enhance the UI for a better user experience.
