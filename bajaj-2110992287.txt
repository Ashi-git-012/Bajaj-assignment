const express = require('express');
const bodyParser = require('body-parser');

const app = express();
const port = process.env.PORT || 3000; 

// Replace with your actual user ID and details (optional)
const userId = "Ashi";
const email = "ashi2287.be21@chitkara.edu.in";
const rollNumber = "2110992287";

app.use(bodyParser.json());

app.post('/bfhl', (req, res) => {
  try {
    const data = req.body.data;
    const evenNumbers = [];
    const oddNumbers = [];
    const alphabets = [];

    for (const item of data) {
      if (typeof item === 'string') {
        alphabets.push(item.toUpperCase());
      } else if (typeof item === 'number') {
        if (item % 2 === 0) {
          evenNumbers.push(item);
        } else {
          oddNumbers.push(item);
        }
      }
    }

    const response = {
      is_success: true,
      user_id: userId,
      email: email,
      roll_number: rollNumber,
      odd_numbers: oddNumbers,
      even_numbers: evenNumbers,
      alphabets: alphabets,
    };

    res.json(response);
  } catch (error) {
    console.error(error);
    res.status(500).json({ is_success: false, message: 'Internal Server Error' });
  }
});

app.listen(port, () => console.log(`Server listening on port 8000`));
