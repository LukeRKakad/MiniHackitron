# Chess Game Reviewer

A modern React application for analyzing chess games from chess.com using Stockfish engine analysis.

## 🎯 Features

### **Import Games**
- Search chess.com players by username
- Browse their recent games
- Automatic PGN parsing and loading
- Displays game metadata (players, time control, result, date)

### **Interactive Game Board**
- Visual chess board with piece rendering
- Navigate through moves step-by-step
- Quick jump to any move in the game
- Reset/Previous/Next/End controls
- Move list with visual highlighting

### **Game Analysis**
- Accuracy percentages for both players
- Blunder and mistake detection
- Best move tracking
- Critical position identification
- Key moments in the game
- Personalized improvement recommendations

### **Statistics Dashboard**
- Side-by-side player comparison
- Mistake breakdown (blunders vs mistakes)
- Best moves analysis
- Game result summary

## 🚀 Getting Started

### Prerequisites
- Node.js 14+
- npm or yarn

### Installation

```bash
# Clone the repository
git clone <repo-url>
cd MiniHackitron

# Install dependencies
npm install

# Start development server
npm start
```

The app will open at `http://localhost:3000`

### Build for Production

```bash
npm run build
```

## 📋 Usage

1. **Import a Game**
   - Enter a chess.com username in the sidebar
   - Click "Search" to fetch their recent games
   - Select a game from the list

2. **Navigate the Game**
   - Use arrow buttons to move through the game
   - Click on moves in the move list to jump to any position
   - Watch the board update in real-time

3. **Analyze the Game**
   - Click "Analyze Game" to generate statistics
   - Review accuracy percentages, mistakes, and key moments
   - Read personalized recommendations for improvement

## 🏗️ Project Structure

```
src/
├── components/
│   ├── GameImporter.js      # Import games from chess.com
│   ├── GameImporter.css
│   ├── GameBoard.js         # Display & navigate the board
│   ├── GameBoard.css
│   ├── GameAnalysis.js      # Show analysis results
│   └── GameAnalysis.css
├── services/
│   └── StockfishAnalyzer.js # Chess engine integration
├── App.js                   # Main application component
├── App.css                  # Global styles
├── index.js                 # React entry point
└── index.css                # Global styles
public/
└── index.html               # HTML template
```

## 🔧 Integrating Stockfish

The current implementation uses mock evaluations. To integrate the real Stockfish engine:

### Step 1: Download Stockfish WASM
```bash
# Download from https://github.com/exodia-info/stockfish-wasm
# Place files in public/stockfish/
```

### Step 2: Create Web Worker

Create `src/workers/StockfishWorker.js`:
```javascript
importScripts('/stockfish/stockfish.js');

let engine;

onmessage = function(e) {
  if (e.data.cmd === 'init') {
    engine = new Stockfish();
    engine.onmessage = (event) => {
      postMessage(event.data);
    };
  } else if (e.data.cmd === 'eval') {
    engine.postMessage(e.data.fen);
  }
};
```

### Step 3: Update StockfishAnalyzer

Modify `evaluateWithStockfish()` method to communicate with the worker.

## 📊 API Integration

The app uses the **chess.com Public API**:
- Fetches games: `/pub/player/{username}/games/{year}/{month}`
- No authentication required
- Rate limiting: Be respectful with requests

## 🎨 Styling

- Modern gradient color scheme (Purple/Indigo)
- Responsive design for mobile and desktop
- Custom chess board styling
- Smooth transitions and hover effects

## 🐛 Known Limitations

1. **Stockfish Integration**: Currently uses mock evaluations. Real Stockfish analysis requires proper WASM setup.
2. **Browser Storage**: Games are not persisted; they load fresh each time.
3. **Analysis Depth**: Mock analysis is simplified; real Stockfish provides deeper insights.

## 📈 Future Enhancements

- [ ] Real Stockfish engine integration
- [ ] Game history and bookmarking
- [ ] Opening and endgame specific analysis
- [ ] Lichess.org support
- [ ] Personalized opening repertoire analysis
- [ ] Blunder heat maps
- [ ] Comparison with other players
- [ ] Export analysis reports (PDF)
- [ ] Dark mode
- [ ] Offline support (PWA)

## 🤝 Contributing

Contributions are welcome! Feel free to:
1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## 📄 License

This project is open source and available under the MIT License.

## 🙏 Acknowledgments

- [chess.com](https://www.chess.com) for providing the Public API
- [Stockfish](https://stockfishchess.org/) - The strongest open-source chess engine
- [chess.js](https://github.com/jhlywa/chess.js) - JavaScript chess library
- React community for excellent documentation

## 📞 Support

For issues, questions, or suggestions, please open a GitHub issue.

---

**Happy analyzing! ♟️**
