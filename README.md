<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Real-Time Stock Ticker</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: black;
      color: white;
      display: flex;
      justify-content: center;
      padding: 20px;
    }

    .ticker-container {
      display: flex;
      gap: 50px;
    }

    table {
      border-collapse: collapse;
      width: 300px;
    }

    th, td {
      padding: 5px 10px;
      text-align: left;
    }

    th {
      color: cyan;
      border-bottom: 1px solid #444;
    }

    .positive {
      color: #0f0; /* green */
    }
    .negative {
      color: #f00; /* red */
    }
    .neutral {
      color: yellow;
    }
  </style>
</head>
<body>
  <div class="ticker-container">
    <table id="leftTable">
      <tr>
        <th>Symbol</th>
        <th>Change</th>
        <th>Last</th>
        <th>Time</th>
      </tr>
    </table>

    <table id="rightTable">
      <tr>
        <th>Symbol</th>
        <th>Change</th>
        <th>Last</th>
        <th>Time</th>
      </tr>
    </table>
  </div>

  <script>
    // Example stock symbols
    const stocks = ["AAPL", "TSLA", "MSFT", "GOOG", "AMZN", "NFLX", "NVDA", "META", "IBM", "ORCL"];

    // Function to simulate stock price & change
    function getRandomStockData(symbol) {
      let price = (Math.random() * 2000).toFixed(2);
      let change = (Math.random() * 4 - 2).toFixed(2); // -2 to +2
      let now = new Date().toLocaleTimeString();

      return {
        symbol,
        change,
        price,
        time: now
      };
    }

    // Function to render data in a table
    function renderTable(tableId, stockData) {
      const table = document.getElementById(tableId);

      // Clear old rows (except header)
      table.innerHTML = `
        <tr>
          <th>Symbol</th>
          <th>Change</th>
          <th>Last</th>
          <th>Time</th>
        </tr>
      `;

      stockData.forEach(stock => {
        let changeClass = "neutral";
        if (stock.change > 0) changeClass = "positive";
        else if (stock.change < 0) changeClass = "negative";

        let row = `
          <tr>
            <td>${stock.symbol}</td>
            <td class="${changeClass}">${stock.change}</td>
            <td>${stock.price}</td>
            <td>${stock.time}</td>
          </tr>
        `;
        table.innerHTML += row;
      });
    }

    function updateTicker() {
      let leftStocks = stocks.slice(0, stocks.length / 2).map(s => getRandomStockData(s));
      let rightStocks = stocks.slice(stocks.length / 2).map(s => getRandomStockData(s));

      renderTable("leftTable", leftStocks);
      renderTable("rightTable", rightStocks);
    }

    // Update every 3 seconds
    updateTicker();
    setInterval(updateTicker, 3000);
  </script>
</body>
</html>
# kaviya
