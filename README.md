# Trading Strategy DSL System

A complete Natural Language → DSL → AST → Python Code → Backtest pipeline for algorithmic trading strategies.

## 🚀 Quick Start

### Prerequisites
- Python 3.8 or higher
- pip package manager

### Installation

1. Clone or download this repository
2. Navigate to project directory:
```bash
   cd trading-dsl
```

3. Install dependencies:
```bash
   pip install -r requirements.txt
```

### Running the Demo
```bash
python main.py
```

Expected output:

================================================================================
TRADING STRATEGY DSL - END-TO-END DEMONSTRATION
...
Total Trades:      12
Total Return:      8.34%
Win Rate:          58.33%

---

## 📚 Features

- ✅ Natural Language Parser - converts English to structured rules
- ✅ Custom DSL - domain-specific language for trading strategies
- ✅ AST Parser - builds abstract syntax tree from DSL
- ✅ Code Generator - converts AST to executable Python
- ✅ Technical Indicators - SMA, RSI, EMA built-in
- ✅ Backtesting Engine - simulates trades with performance metrics

---

## 🧪 Running Tests

### Run all tests:
```bash
python -m pytest tests/ -v
```

### Run specific test file:
```bash
python tests/test_system.py
```

### Expected test output:
test_nl_parser ... PASSED
test_dsl_generation ... PASSED
test_dsl_parser ... PASSED
test_code_generator ... PASSED
test_backtester ... PASSED
test_end_to_end ... PASSED

---

## 📖 Usage Examples

### Example 1: Simple Price Threshold
```python
from main import *

nl_input = "Buy when close is above 100"

# Run pipeline
nl_parser = NLParser()
json_rules = nl_parser.parse(nl_input)

dsl_gen = DSLGenerator()
dsl_text = dsl_gen.generate(json_rules)

dsl_parser = DSLParser()
ast = dsl_parser.parse(dsl_text)

df = create_sample_data()
code_gen = CodeGenerator()
entry, exit = code_gen.generate(ast, df)

bt = Backtester(df)
results = bt.run(entry, exit)

print(f"Total Return: {results['total_return']}%")
```

### Example 2: Moving Average Crossover
```python
nl_input = """
Buy when close is above 20-day moving average and volume is above 1 million.
Exit when RSI(14) is below 30.
"""
# ... same pipeline as above
```

### Example 3: RSI Strategy
```python
nl_input = "Enter when RSI(14) is below 30. Exit when RSI(14) is above 70."
# ... same pipeline
```

---

## 🎯 Supported Features

### Indicators
- **SMA(period)** - Simple Moving Average
- **EMA(period)** - Exponential Moving Average
- **RSI(period)** - Relative Strength Index
- **PCT_CHANGE()** - Percentage Change

### Operators
- `>`, `<`, `>=`, `<=`, `==` - Comparison operators
- `AND`, `OR` - Logical operators

### Data Fields
- `open`, `high`, `low`, `close`, `volume`
- Lookback syntax: `high[-1]` (yesterday's high)

### Special Functions
- **CROSS(series, threshold, direction)** - Cross above/below events
- **PCT_CHANGE(series)** - Percentage change detection

---

## 🏗️ Architecture

### Pipeline Flow
Natural Language → NL Parser → JSON
↓
DSL Generator → DSL Text
↓
DSL Parser → AST
↓
Code Generator → Signals
↓
Backtester → Results

### Components

1. **NL Parser** (`NLParser` class)
   - Converts natural language to structured JSON
   - Uses regex pattern matching
   - Handles indicators, operators, and values

2. **DSL Generator** (`DSLGenerator` class)
   - Creates DSL text from JSON structure
   - Produces human-readable trading rules

3. **DSL Parser** (`DSLParser` class)
   - Parses DSL text into Abstract Syntax Tree
   - Validates syntax
   - Builds structured node objects

4. **Code Generator** (`CodeGenerator` class)
   - Converts AST to pandas operations
   - Evaluates conditions vectorized
   - Returns boolean signals

5. **Backtester** (`Backtester` class)
   - Simulates trading based on signals
   - Tracks positions and P&L
   - Calculates performance metrics

---

## 📊 Performance Metrics

The backtester calculates:
- **Total Return** - Overall percentage gain/loss
- **Win Rate** - Percentage of profitable trades
- **Average Return** - Mean return per trade
- **Max Drawdown** - Largest peak-to-trough decline
- **Trade Count** - Total number of trades executed
- **Complete Trade Log** - Entry/exit details for each trade

---

## 📁 Project Structure
trading-dsl/
├── main.py              # Complete system implementation
├── demo.py              # Demonstration script
├── tests/               # Test suite
│   └── test_system.py
├── examples/            # Example strategies
│   └── sample_strategies.txt
├── data/                # Sample data files
└── docs/                # Documentation
├── README.md
└── DSL_SPECIFICATION.md

---

## 🔧 Customization

### Adding New Indicators

Edit the `Indicators` class in `main.py`:
```python
class Indicators:
    @staticmethod
    def macd(series, fast=12, slow=26):
        fast_ema = series.ewm(span=fast).mean()
        slow_ema = series.ewm(span=slow).mean()
        return fast_ema - slow_ema
```

### Adding New Operators

Edit `CodeGenerator._evaluate_node()`:
```python
if node.operator == '!=':
    return left_val != right_val
```

### Extending NL Parser

Add new patterns to `NLParser.__init__()`:
```python
self.indicator_patterns = {
    r'macd': 'macd',
    # ... existing patterns
}
```

---

## 🐛 Troubleshooting

### Issue: "No module named 'pandas'"
**Solution:**
```bash
pip install pandas numpy
```

### Issue: "python is not recognized"
**Solution:**
- Use `python3` instead: `python3 main.py`
- Or reinstall Python with "Add to PATH" checked

### Issue: Import errors
**Solution:**
Make sure you're in the correct directory:
```bash
cd trading-dsl
python main.py
```

---

## 📄 License

MIT License - Feel free to use for educational purposes

---

## 👤 Author

Shravani Patil
shravanipatil580@gmail.com 

Assignment: NLP → DSL → Strategy Execution Prototype
Date: December 2024

---

## 🙏 Acknowledgments

- Assignment requirements provided by Rotally AI
- Built using Python, Pandas, NumPy
- Inspired by production trading systems

---

## 📞 Support

For questions or issues:
1. Check the troubleshooting section
2. Review DSL_SPECIFICATION.md for grammar details
3. Run tests to verify installation: `python tests/test_system.py`
