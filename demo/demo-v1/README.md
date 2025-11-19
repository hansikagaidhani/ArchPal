# ArchPal AI Companion Demo v1

A Streamlit application that provides a chat interface with Anthropic Claude via LangChain, designed for research demos with student interaction tracking and privacy-preserving data export.

## Features

- **Startup Form**: Collects student information (first name, last name, college year, major, session number) and assigns unique identifiers
- **Session Password Protection**: Password-protected access to ensure only authorized participants
- **Chat Interface**: Powered by Anthropic Claude via LangChain with customizable system prompts
- **Message Logging**: Tracks all messages with timestamps for the duration of the session
- **Admin Controls**: Admin panel for customizing system prompts and role settings
- **Consent & Privacy**: Export consent form with data privacy acknowledgment
- **Dual CSV Export**: Exports anonymized conversation data and identifier files separately
- **Dropbox Integration**: Automatic CSV export to Dropbox with separate folders for anonymized and identifier data
- **Input Validation**: Automatic trimming of trailing spaces from form inputs

## Setup

1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Configure secrets (required):
   - Set up Dropbox API (see `EXPORT_SETUP.md` for detailed instructions)
   - Create `.streamlit/secrets.toml` in your project root
   - Add required configuration (see `EXPORT_SETUP.md` for details)
   - Copy from `.streamlit/secrets.toml.example` if needed

3. Run the application:
```bash
streamlit run app.py
```

4. Fill out the startup form with student information and session password

5. Start chatting with ArchPal!

6. Export conversation data when ready (requires consent form acknowledgment)

## Research Features

### Student Information Collection
- On first launch, students fill out a form with:
  - First Name
  - Last Name
  - College Year (dropdown selection)
  - Major
  - Session Number
  - Session Password (for access control)
- System automatically generates a unique identifier (UUID) for each session
- Input validation: Trailing spaces are automatically trimmed from text inputs
- This information is included in the system prompt and export files

### Message Tracking
- All messages are logged with timestamps
- Messages are stored for the duration of the Streamlit session
- Both student and ArchPal messages are tracked with separate timestamps
- Message log includes: user message, user message time, AI message, AI message time

### Admin Controls
- Admin login panel for authorized personnel
- Customizable system prompt and role settings
- Ability to reinitialize the LLM with new prompts
- Configuration export functionality

### Export Format

The application exports **two separate CSV files** for privacy-preserving research:

1. **Anonymized Conversation CSV** (Folder 1):
   - Full conversation data with student names replaced by `[NAME]`
   - Columns: Unique Identifier, College Year, Major, userMessage, userMessageTime, AIMessage, AIMessageTime
   - File naming: `{unique_id}_Session{session_number}.csv`

2. **Identifier CSV** (Folder 2):
   - Single row with identifying information for matching
   - Columns: first_name, last_name, unique_id
   - File naming: `{unique_id}_identifier.csv`
   - Used for matching anonymized conversations with consent forms

Both files share the same `unique_id` for matching while keeping conversation data anonymized.

### Privacy & Consent
- Export requires explicit consent form acknowledgment
- Data privacy explanation before export
- Separate storage of anonymized and identifying data
- Only anonymized data is used for research purposes

See `EXPORT_SETUP.md` for detailed information about CSV formats and Dropbox configuration.

## Configuration

The app uses Streamlit secrets for secure configuration. Required secrets include:

- **Anthropic API Key**: For chatbot functionality
- **Dropbox API Credentials**: For automatic CSV export
- **Session Password**: For access control
- **Admin Credentials**: For admin panel access
- **Dropbox Folder Paths**: Two separate folders for anonymized and identifier data

See `EXPORT_SETUP.md` for detailed setup instructions for both local development and Streamlit Cloud deployment.

## Additional Tools

- **master_list_assembly.py**: Utility script to combine identifier CSV files from a folder with an existing master list
- **data_extractor.py**: Utility script for processing student data from exported files

## Privacy & Data Handling

- Student names are automatically anonymized in conversation exports
- Identifying information is stored separately from conversation data
- Both files use the same unique identifier for matching purposes
- Export requires explicit user consent and privacy acknowledgment
