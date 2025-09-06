# Skillcred-Hackathon
# Question Generator App

A full-stack application that generates multiple-choice questions from text, images, or PDF documents using Google's Gemini AI.

## Features

- **Multi-format Input**: Accepts text input, image files (PNG, JPG, JPEG), and PDF documents
- **AI-Powered**: Uses Google Gemini AI to generate high-quality multiple-choice questions
- **Interactive UI**: Clean chat-like interface with real-time question generation
- **Answer Validation**: Users can select answers and get immediate feedback
- **Error Handling**: Comprehensive error handling and user feedback
- **Security**: File upload validation and sanitization

## Tech Stack

### Backend
- **FastAPI**: Modern Python web framework
- **Google Gemini AI**: AI question generation
- **Pytesseract**: OCR for image text extraction
- **PDFplumber**: PDF text extraction
- **Uvicorn**: ASGI server

### Frontend
- **React**: User interface framework
- **Vite**: Build tool and dev server
- **Axios**: HTTP client for API calls
- **CSS**: Custom styling with dark theme

## Setup Instructions

### Prerequisites

- Python 3.8+
- Node.js 16+
- Google Gemini API key
- Tesseract OCR (for image processing)

### Backend Setup

1. **Navigate to backend directory**:
   ```bash
   cd backend
   ```

2. **Create virtual environment**:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables**:
   Create a `.env` file in the backend directory:
   ```env
   GOOGLE_API_KEY=your_gemini_api_key_here
   GEMINI_MODEL=gemini-1.5-flash
   UPLOAD_FOLDER=uploads
   MAX_FILE_SIZE=16777216
   ALLOWED_ORIGINS=http://localhost:3000
   ```

5. **Install Tesseract OCR**:
   - **Windows**: Download from [UB-Mannheim/tesseract](https://github.com/UB-Mannheim/tesseract/wiki)
   - **macOS**: `brew install tesseract`
   - **Linux**: `sudo apt-get install tesseract-ocr`

6. **Run the backend server**:
   ```bash
   python app.py
   ```
   Server will start on `http://localhost:5000`

### Frontend Setup

1. **Navigate to frontend directory**:
   ```bash
   cd frontend
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Set up environment variables**:
   Create a `.env` file in the frontend directory:
   ```env
   VITE_API_URL=http://localhost:5000
   VITE_DEBUG=true
   ```

4. **Start development server**:
   ```bash
   npm run dev
   ```
   App will be available at `http://localhost:3000`

## Usage

1. **Start the application**: Open `http://localhost:3000` in your browser
2. **Provide input**:
   - Type text in the message box, or
   - Upload an image (PNG, JPG, JPEG) containing text, or
   - Upload a PDF document
3. **Set quantity**: Choose how many questions to generate (1-20)
4. **Generate**: Click "Send" to generate questions
5. **Interact**: Select answers to see if they're correct

## API Endpoints

### POST `/generate-questions`
Generate multiple-choice questions from input.

**Parameters**:
- `inputData` (string): Text input
- `quantity` (int): Number of questions (1-20)
- `file` (file): Optional image or PDF file

**Response**:
```json
{
  "questions": [
    {
      "question": "What is...",
      "options": ["Option A", "Option B", "Option C", "Option D"],
      "answer": "Correct answer"
    }
  ],
  "input_length": 123
}
```

### GET `/health`
Health check endpoint.

**Response**:
```json
{
  "status": "healthy",
  "version": "1.0.0"
}
```

## Error Handling

The application provides detailed error messages for:
- Invalid file types/sizes
- API timeouts
- Network issues
- Server errors
- Input validation failures

## Security Features

- File upload validation and sanitization
- CORS configuration for production
- File size limits (16MB max)
- Input validation and sanitization
- Secure file handling with automatic cleanup

## Development

### Backend Development
- Use `python app.py` to run development server
- Logs are available in console with timestamps
- File uploads are automatically cleaned up after processing

### Frontend Development
- Use `npm run dev` for development server with hot reload
- Environment variables are configured in `.env` files
- API errors are handled with user-friendly messages

## Production Deployment

### Backend
1. Set production environment variables:
   ```env
   ALLOWED_ORIGINS=https://your-frontend-domain.com
   ```
2. Use production ASGI server (e.g., Gunicorn with Uvicorn workers)

### Frontend
1. Build for production:
   ```bash
   npm run build
   ```
2. Set production API URL:
   ```env
   VITE_API_URL=https://your-api-domain.com
   ```

## Troubleshooting

### Common Issues

1. **OCR not working**: Ensure Tesseract is installed and in PATH
2. **API key errors**: Verify Google Gemini API key is valid
3. **File upload issues**: Check file size and type restrictions
4. **CORS errors**: Verify ALLOWED_ORIGINS environment variable

### Getting Help

Check the browser console and backend logs for detailed error information. Ensure all dependencies are properly installed and environment variables are set.

## License

This project is for educational/demonstration purposes. Please ensure you comply with Google's Gemini API terms of service.
