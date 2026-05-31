# J.A.R.V.I.S. 🤖 AI Assistant

**Just A Rather Very Intelligent System**

A fully functional, production-ready desktop AI assistant inspired by Iron Man's J.A.R.V.I.S. Built with Python, featuring voice interaction, real AI intelligence, system control, and a modern cyberpunk UI.

---

## ✨ Features

### 🎤 Voice Interaction
- Continuous listening mode & push-to-talk
- Wake word detection ("Jarvis")
- Real-time speech recognition (Google SR / Whisper)
- Animated audio waveform visualization

### 🧠 Real AI Intelligence
- Connects to **OpenAI** (GPT-4o, GPT-4, GPT-3.5)
- Connects to **OpenRouter** (access to 200+ models: Claude, Gemini, Llama, Mistral, DeepSeek, Qwen...)
- Local fallback when no API is configured
- Full conversation memory & context awareness
- Dynamic natural language responses (NO scripted commands)

### 🔊 Voice Output (15+ Voices)
- **Edge-TTS**: 15 high-quality neural voices (US, UK, AU, CA, IN, IE, SG)
- **pyttsx3**: Offline fallback with system voices
- Dynamic voice switching via Settings panel
- Adjustable speech rate & volume
- Test voice button

### 🖥️ System Control (Safe Mode)
- Open/close applications by name
- File search across system
- Volume & brightness control
- Power commands (shutdown, restart, lock, sleep)
- Screenshot capture
- **All actions require explicit user permission**
- Granular command allowlist

### 📊 Real-Time System Monitor
- CPU usage per core + frequency
- RAM usage with GB breakdown
- Disk usage
- Network speed (download/upload)
- Battery status
- Process count
- Temperature sensors

### 🎨 Modern Dark UI
- Iron Man HUD-inspired design
- Cyan/neon color scheme
- Animated waveform when speaking
- Status indicators (Listening / Thinking / Speaking)
- Chat bubble conversation display
- Circular progress stats

### 💾 Memory System
- Persistent conversation history (JSON)
- Multiple conversation support
- Create, switch, delete conversations
- Export conversations to JSON
- Configurable history limit

### ⚙️ Settings Panel
- API key configuration (OpenAI / OpenRouter)
- Model selection with 200+ options
- Voice selection with test
- Microphone & wake word settings
- System control permissions
- Memory preferences

### 🔌 Plugin System
- Extensible architecture
- Load/unload plugins dynamically
- Built-in Web Search & Timer plugins
- Easy to create new plugins

---

## 🚀 Quick Start

### 1. Prerequisites
- Python 3.8+
- Windows, macOS, or Linux
- Microphone (for voice input)
- Speakers/headphones (for TTS output)

### 2. Install Dependencies
```bash
cd jarvis_assistant
pip install -r requirements.txt
```

**Platform-specific:**
- **Windows**: `pip install pyaudio` (or use pre-built wheel)
- **Linux**: `sudo apt-get install portaudio19-dev python3-pyaudio`
- **macOS**: `brew install portaudio`

### 3. Run
```bash
python main.py
```

### 4. Configure API Key
1. Click the **⚙** button in the top-right corner
2. Go to **AI API** tab
3. Select **OpenRouter** (recommended) or **OpenAI**
4. Enter your API key
5. Choose a model
6. Click **Save & Close**

> **Get a free API key:** [OpenRouter](https://openrouter.ai/keys) — works with 200+ models

---

## 🎯 Usage Examples

### Voice Commands
Say or type:
- *"Hello Jarvis"*
- *"What's the weather like?"*
- *"Open Chrome"*
- *"Search for my resume"*
- *"Volume up"*
- *"How is my system doing?"*
- *"Set a timer for 5 minutes"*
- *"Take a screenshot"*
- *"Lock my computer"*

### Keyboard Shortcuts
- **Enter**: Send typed message
- **Shift+Enter**: New line in input
- **Space** (when configured): Push-to-talk

---

## 📁 Project Structure

```
jarvis_assistant/
├── main.py                  # Entry point
├── build_exe.py             # PyInstaller build script
├── requirements.txt         # Dependencies
├── Jarvis.spec              # PyInstaller spec (auto-generated)
│
├── config/
│   ├── __init__.py          # Configuration manager
│   └── settings.json        # Persisted settings
│
├── modules/
│   ├── __init__.py
│   ├── voice_input.py       # Speech recognition (Whisper/Google)
│   ├── ai_brain.py          # LLM integration (OpenAI/OpenRouter)
│   ├── tts_engine.py        # Text-to-speech (Edge-TTS/pyttsx3)
│   ├── system_control.py    # System automation (safe mode)
│   ├── system_monitor.py    # Real-time system stats (psutil)
│   ├── memory.py            # Conversation persistence
│   └── wake_word.py         # Wake word detection
│
├── ui/
│   ├── __init__.py
│   ├── main_window.py       # Main application window
│   ├── styles.py            # Dark theme stylesheet
│   ├── settings_dialog.py   # Settings panel
│   └── stats_widget.py      # System stats display
│
├── plugins/
│   ├── __init__.py
│   └── plugin_base.py       # Plugin system + example plugins
│
├── memory/                  # Conversation storage
└── assets/                  # Icons and resources
```

---

## 📦 Building to .EXE

### Windows Executable

1. Install build tools:
```bash
pip install pyinstaller
```

2. Run the build script:
```bash
python build_exe.py
```

3. Find your executable in:
```
dist/Jarvis.exe
```

### Manual Build with PyInstaller
```bash
pyinstaller --name=Jarvis --onefile --windowed --noconfirm --clean main.py
```

### Build Options
- `--onefile`: Single .exe file
- `--windowed`: No console window (GUI only)
- `--add-data "config/settings.json;config"`: Include config
- `--icon=assets/jarvis_icon.png`: Custom icon

---

## 🔧 Configuration

### settings.json
All settings are stored in `config/settings.json`:

```json
{
  "api": {
    "provider": "openrouter",
    "openrouter_key": "sk-or-v1-...",
    "model": "openai/gpt-4o-mini",
    "temperature": 0.7,
    "max_tokens": 1024
  },
  "voice": {
    "engine": "edge_tts",
    "voice_id": "en-US-GuyNeural",
    "rate": 0,
    "volume": 1.0
  },
  "microphone": {
    "enabled": true,
    "continuous_listening": true,
    "wake_word_enabled": false,
    "wake_word": "jarvis"
  },
  "system_control": {
    "enabled": true,
    "require_confirmation": true,
    "allowed_commands": ["open", "close", "volume", ...]
  },
  "memory": {
    "enabled": true,
    "max_history": 50
  }
}
```

---

## 🤝 Creating Plugins

Extend Jarvis with custom skills:

```python
from plugins.plugin_base import JarvisPlugin

class MyPlugin(JarvisPlugin):
    def get_name(self): return "My Skill"
    def get_description(self): return "Description"
    def get_version(self): return "1.0.0"
    
    def on_voice_command(self, text):
        if "my trigger" in text.lower():
            return "Response from my plugin!"
        return None
```

Save as `plugins/my_plugin.py` — auto-loaded on next startup.

---

## 🛡️ Security & Privacy

- **No malware behavior.** All system actions require explicit user permission.
- **API keys stored locally** in `config/settings.json`
- **Conversation history stored locally** in `memory/`
- **No telemetry, no analytics, no data collection**
- **Microphone only active** when listening mode is enabled
- **Network requests only** to configured API endpoints

---

## ⚡ Supported AI Models

### Via OpenRouter (200+ models):
- OpenAI: GPT-4o, GPT-4o-mini, GPT-4, GPT-3.5
- Anthropic: Claude 3.5 Sonnet, Claude 3 Opus
- Google: Gemini 2.0 Flash, Gemini 1.5 Pro
- Meta: Llama 3.1 (8B/70B/405B)
- Mistral: Mistral 7B, Mixtral 8x22B
- DeepSeek: DeepSeek V2, DeepSeek Coder
- Qwen: Qwen 2.5 (7B/72B)
- Many more...

### Via OpenAI:
- GPT-4o, GPT-4o-mini, GPT-4 Turbo, GPT-3.5 Turbo

### Via Ollama (local):
- Any local model running on Ollama

---

## 🖥️ System Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| CPU | 2 cores | 4+ cores |
| RAM | 2 GB | 8 GB |
| Storage | 200 MB | 500 MB |
| OS | Windows 10 / Ubuntu 20.04 / macOS 11 | Latest |
| Microphone | Required for voice | USB headset preferred |
| Internet | Required for API | Broadband |

---

## 📝 License

MIT License - Free for personal and commercial use.

---

## 🙏 Acknowledgements

- Inspired by J.A.R.V.I.S. from Marvel's Iron Man
- Built with PyQt5, edge-tts, OpenAI, and many open-source libraries
- Special thanks to the Python community

---

*"Sometimes you gotta run before you can walk." - Tony Stark*
