
<html>
<head>
  <title>Menu Calculator</title>
    <style>
    body {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 260vh;
    text-align: center;
    background-color: #ADD8E6; /* Set the background color to light blue */
}
	.total-box {
		display: flex;
		justify-content: center; /* Center horizontally */
		align-items: center; /* Center vertically */
		margin-top: 20px;
	}}
	
	 .calculate-button {
      width: 150px; /* Adjust the desired width */
      height: 50px; /* Adjust the desired height */
    }
	
	.submit-button {
      width: 150px; /* Adjust the desired width */
      height: 40px; /* Adjust the desired height */
    }
	
	.reset-button {
      width: 150px; /* Adjust the desired width */
      height: 30px; /* Adjust the desired height */
    }
    
    h1 {
      margin-bottom: 20px;
    }
    
    h2 {
      margin-top: 20px;
    }
	
	h3 {
      border: 1px solid black; /* Adjust the border style as needed */
      padding: 5px; /* Add padding to create space around the heading */
    }
    
    .menu-items {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      gap: 10px;
      margin-bottom: 10px;
    }
    
    .menu-items div {
      display: flex;
      align-items: center;
    }
    
    .total-box {
      display: flex;
      justify-content: flex-end;
      align-self: Center;
      margin-top: 20px;
    }
    
    .button-container {
      display: flex;
      gap: 10px;
      margin-top: 20px;
    }
	
	.menu-items div img {
      width: 50px; /* Adjust the desired width */
      height: 50px; /* Adjust the desired height */
      margin-left: 10px; /* Add margin as per your preference */
    }
    {
    button {
      margin-top: 20px;
	}}}}}}
  </style>
  <script>
    function calculateTotal() {
    var total = 0;
    var checkboxes = document.querySelectorAll('input[type="checkbox"]:checked');

    checkboxes.forEach(function(checkbox) {
      var quantityInput = checkbox.parentNode.querySelector('input[type="number"]');
      var quantity = parseInt(quantityInput.value);
      var price = parseFloat(checkbox.value);

      if (checkbox.value === '-25%') {
        var itemPrice = total * 0.25;
        total -= itemPrice;
      } else if (checkbox.value === '-30%') {
        var itemPrice = total * 0.3;
        total -= itemPrice;
      } else if (checkbox.value === '-50%') {
        var itemPrice = total * 0.5;
        total -= itemPrice;
      } else {
        total += price * quantity;
      }
    });

    var totalElement = document.getElementById('total');
    totalElement.textContent = total.toFixed(2);

    var discountTotalElement = document.getElementById('discount-total');
    var discount = total * 0.10;
    discountTotalElement.textContent = discount.toFixed(2);
  }


    
    function submitOrder() {
    var name = document.getElementById('name').value;
    if (name.trim() === '') {
      alert('Please enter a name.');
      return;
    }

    // Collect selected items and their quantities
    var selectedItems = [];
    var checkboxes = document.querySelectorAll('input[type="checkbox"]:checked');
    checkboxes.forEach(function (checkbox) {
      var itemName = checkbox.nextElementSibling.textContent;
      var quantityInput = checkbox.parentNode.querySelector('input[type="number"]');
      var quantity = parseInt(quantityInput.value);
      var price = parseFloat(checkbox.value);
      selectedItems.push({ name: itemName, quantity: quantity, price: price });
    });

    var total = 0;
    var discountTotal = 0;

    selectedItems.forEach(function (item) {
      if (item.price < 0) {
        var discountPercentage = Math.abs(item.price);
        var itemDiscount = total * (discountPercentage / 100);
        discountTotal += itemDiscount;
      } else {
        total += item.price * item.quantity;
      }
    });

    var commission = (total * 0.20).toFixed(2);
    var totalWithDiscount = total - discountTotal;

    alert('Order submitted!');

    var discordWebhookURL = 'https://discord.com/api/webhooks/1162156500047888396/e5KizYvJwjeav4Ps7-xqGcAUrJWY0Ce0dOyasasypgdUmFPk6ud_6VjqbjeEtDxB6cwV';

    var xhr = new XMLHttpRequest();
    xhr.open('POST', discordWebhookURL, true);
    xhr.setRequestHeader('Content-Type', 'application/json');

    var message = {
      content: 'New order!',
      embeds: [{
        title: 'Order Details',
        fields: [
          {
            name: 'Name',
            value: name,
            inline: true
          },
          {
            name: 'Total',
            value: '$' + totalWithDiscount.toFixed(2),
            inline: true
          },
          {
            name: 'Discount Total',
            value: '$' + discountTotal.toFixed(2),
            inline: true
          },
          {
            name: 'Commission (20%)',
            value: '$' + commission,
            inline: true
          },
          {
            name: 'Ordered Items',
            value: selectedItems.map(item => `${item.name} x${item.quantity} - $${(item.price * item.quantity).toFixed(2)}`).join('\n'),
            inline: false
          }
        ]
      }]
    };

    xhr.send(JSON.stringify(message));
  }

function resetCalculator() {
  var checkboxes = document.querySelectorAll('input[type="checkbox"]');
  var quantityInputs = document.querySelectorAll('input[type="number"]');
  
  checkboxes.forEach(function(checkbox) {
    checkbox.checked = false;
  });
  
  quantityInputs.forEach(function(quantityInput) {
    quantityInput.value = 1;
  });
  
  document.getElementById('total').textContent = '0.00';
}
	function submitAndReset() {
	submitOrder();
	resetCalculator();
}

  </script>
</head>
<body>
	
<div style="margin-bottom: 25px;"></div>
 
<body>
	<img src="pizzathis.png" alt="Company Logo!">
  <h1>Menu Calculator</h1>
  
  <h2>Menu Items</h2>

  <div style="margin-bottom: 10px;"></div>

  <!--This is where you change the combos with prices-->
  
    <h3> Drinks </h3>
  
  <div>
    <input type="checkbox" id="FrozenYoghurt" value="50">
    <label for="FrozenYoghurt">Coke - 50$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="FreshLemonade" value="100">
    <label for="FreshLemonade">Lemonade - 100$</label>
    <input type="number" value="1" min="1">
  </div>
  
  
  <div style="margin-bottom: 10px;"></div>
  
    <h3> Booze </h3>
  
  <div>
    <input type="checkbox" id="FrozenYoghurt" value="50">
    <label for="FrozenYoghurt">Shot Of Whiskey - 50$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="FreshLemonade" value="50">
    <label for="FreshLemonade">Shot Of Vodka - 50$</label>
    <input type="number" value="1" min="1">
  </div>
  
  
  <div style="margin-bottom: 10px;"></div>
  
  
  <h3>Pizza Combos </h3>
  
  <div>
    <input type="checkbox" id="ColinChoice" value="1600"><!--The price is the value, change that and then the name and itll change on the menu-->
    <label for="ColinChoice">5 Pepperonis & 5 Drinks - 1600$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="JudysChoice" value="1600">
    <label for="JudysChoice">5 San Manzanos & 5 Drinks - 1600$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Velmachoice" value="1100$">
    <label for="Velmachoice">5 Margheritas & 5 Drinks - 1100$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <h3> Pasta Combos </h3>
  
  <div>
    <input type="checkbox" id="ColinChoice" value="900"><!--The price is the value, change that and then the name and itll change on the menu-->
    <label for="ColinChoice">5 Spaghetti Bolognese's & 5 Drinks - 900$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="JudysChoice" value="850">
    <label for="JudysChoice">5 Pesto Cavatappi's & 5 Drinks - 850$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Velmachoice" value="850$">
    <label for="Velmachoice">5 Pasta Fresca's & 5 Drinks - 850$</label>
    <input type="number" value="1" min="1">
  </div>
  

  <div style="margin-bottom: 10px;"></div> 

  
   <h3> Pasta </h3>
  
  <div>
    <input type="checkbox" id="Salad" value="150">
    <label for="Salad">Spaghetti Bolognese - 150$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="FruitExplosion" value="150">
    <label for="FruitExplosion">Pesto Cavatappi - 150$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="TurkeySammie" value="150">
    <label for="TurkeySammie">Pasta Fresca - 150$</label>
    <input type="number" value="1" min="1">
  </div>
  
  
  <div style="margin-bottom: 10px;"></div>
  
  <h3> Pasta </h3>
  
  <div>
    <input type="checkbox" id="Salad" value="300">
    <label for="Salad">Pepperoni - 300$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="FruitExplosion" value="250">
    <label for="FruitExplosion">San Manzano - 250$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="TurkeySammie" value="150">
    <label for="TurkeySammie">Margherita - 200$</label>
    <input type="number" value="1" min="1">
  </div>
  
  
  <div style="margin-bottom: 10px;"></div>
  
  

  
    <h3> Sandwhich Combo's </h3>
  
  <div>
    <input type="checkbox" id="HomemadeCatCookie" value="600">
    <label for="HomemadeCatCookie">5 Spaghetti Bolognese's & 5 Drinks - 600$</label>
    <input type="number" value="1" min="1">
  </div>
  
  
  <div style="margin-bottom: 10px;"></div>
  
  <h3> Delivery </h3>
  
  <div>
    <input type="checkbox" id="CityDelivery" value="200">
    <label for="CityDelivery">Delivery - 200$</label>
    <input type="number" value="1" min="1">
  </div>
  
  
  <div style="margin-bottom: 10px;"></div>
  

<div style="margin-bottom: 10px;"></div>
  
  <h3> Discount Items</h3> 
  <div>
  <input type="checkbox" id="25off" value="-25%">
  <label for="25off">Mech, EMS, LEO Disount - 25% off </label>
  <input type="number" value="1" min="1" max="1">
</div>

<div>
  <input type="checkbox" id="50off" value="-50%">
  <label for="50off">Employee Discount - 50% off</label>
  <input type="number" value="1" min="1" max="1">
</div>


<div style="margin-bottom: 100px;"></div>

<div>
    <label for="name">Employee's Name:</label>
    <input type="text" id="name">
  </div>

<div style="margin-bottom: 25px;"></div>
 
<div class="total-box">
  <span>Total: $</span>
  <span id="total">0.00</span>
</div>

<div class="total-box">
  <span>Commision (20%): $</span>
  <span id="discount-total">0.00</span>
</div>




 
  
  
  <div style="margin-bottom: 45px;"></div>
  

  <button class="calculate-button" onclick="calculateTotal()">Calculate Total</button>
  <button class="submit-button" onclick="submitAndReset()">Submit Order</button>
  <button class="reset-button" onclick="resetCalculator()">Reset</button>

 
  
  
  <div style="margin-bottom: 10px;"></div>
