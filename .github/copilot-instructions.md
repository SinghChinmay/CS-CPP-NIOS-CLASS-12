# Copilot Instructions

## Project Overview

This is an educational web application for **NIOS Class 12 Computer Science - C++ MCQ Quiz System**. It's a single-page interactive quiz application with dropdown-based topic selection that dynamically loads questions from JSON files and provides immediate feedback with explanations.

## Architecture

### Core Components
- **`index.html`** - Complete SPA with embedded CSS/JS and dropdown selector
- **`Control_Statements_MCQ.json`** - Question database for Lesson 14 (606 lines, 48 questions)
- **`Functions_MCQ.json`** - Question database for Lesson 15 (48 questions)
- **`text.txt`** - Source material from NIOS Module 3 Functions (808 lines)

### Data Flow
```
Quiz Selector Dropdown → JSON File Selection → Fetch API → Dynamic DOM → User Interaction → Score Calculation
```

## Key Patterns & Conventions

### Quiz JSON Structure
```json
{
  "title": "Topic Name - Multiple Choice Questions",
  "subtitle": "NIOS Class 12 Computer Science - Lesson X",
  "questions": [...]
}
```

### Question Data Schema
```json
{
  "id": number,
  "question": "string",
  "options": ["option1", "option2", "option3", "option4"], 
  "correctAnswer": number, // 0-indexed
  "explanation": "detailed explanation string"
}
```

### DOM ID Conventions
- Question containers: `question-${questionId}`
- Option elements: `option-${questionId}-${optionIndex}`
- Answer sections: `answer-${questionId}`
- Explanation sections: `explanation-${questionId}`

### State Management
- `quizData` - Loaded JSON structure
- `userAnswers` - Object mapping `questionId → selectedIndex`
- `totalQuestions` - Question count for scoring

### CSS Classes for State
- `.selected` - User's chosen option
- `.correct` - Correct answer (green)
- `.incorrect` - Wrong answer (red)
- `.show` - Reveals hidden sections (answers/explanations)

## Development Workflows

### Creating New MCQ JSON Files from Text Content

**When given a text file with educational content:**

1. **Analyze Source Material**
   - Read the entire text file to understand topics covered
   - Identify key concepts, definitions, syntax, functions, etc.
   - Note NIOS lesson number and module information

2. **Generate Comprehensive MCQs**
   - Create 40-50 questions covering all major topics
   - Follow the established JSON schema exactly
   - Ensure sequential numbering starting from 1
   - Use 0-indexed correctAnswer values

3. **Question Types to Include**
   - **Conceptual**: "What is...?", "Which statement is true...?"
   - **Functional**: "What does function X do?", "Which header file...?"
   - **Syntax**: "How do you declare...?", "What symbol is used...?"
   - **Comparative**: "What is the difference between...?"
   - **Applied**: Code output questions, parameter passing scenarios

4. **MCQ Quality Standards**
   - Clear, unambiguous question stems
   - Four distinct options (A, B, C, D)
   - One clearly correct answer
   - Detailed explanations for educational value
   - Cover both basic and advanced concepts

5. **File Naming Convention**
   - Format: `{Topic}_MCQ.json`
   - Examples: `Functions_MCQ.json`, `Arrays_MCQ.json`, `Classes_MCQ.json`

6. **Update HTML Dropdown**
   - Add new option to quiz selector dropdown
   - Use descriptive names: "Topic Name (Lesson X)"
   - Maintain lesson number order

### Adding New Questions to Existing Files
1. Add to appropriate JSON file following schema
2. Ensure sequential IDs and 0-indexed `correctAnswer`
3. Test explanation rendering and answer feedback

### UI Modifications
- All styling is embedded in `<style>` section
- JavaScript functions handle dynamic loading
- Gradient themes: `#667eea` to `#764ba2`
- Responsive design for mobile devices

### Testing Locally
- Serve via local HTTP server (required for fetch API)
- Common: `python -m http.server 8000` or Live Server extension
- Access: `http://localhost:8000`
- Test dropdown functionality and JSON loading

## Educational Content Context

### Current Topics Available
- **Lesson 14**: Control Statements (if, switch, loops, jumps)
- **Lesson 15**: Functions (library functions, user-defined, parameters, scope)

### Content Sources
- NIOS Class 12 Computer Science modules
- Official curriculum materials
- Comprehensive coverage of C++ programming concepts

### Question Distribution Standards
- 40-50 questions per topic for thorough coverage
- Mix of difficulty levels (basic, intermediate, advanced)
- Each question includes detailed educational explanations
- Covers syntax, concepts, and practical applications

## File Dependencies

- **No external libraries** - Pure HTML/CSS/JavaScript
- **Fetch API** dependency on JSON files
- **Modern browser** features (async/await, template literals)
- **Local server** required for file loading

## Coding Standards

- **Function naming**: camelCase (`loadSelectedQuiz`, `createQuestionCard`)
- **Element creation**: `document.createElement()` with property assignment
- **Event handling**: Inline onclick attributes for simplicity
- **Error handling**: Comprehensive try-catch for JSON loading
- **State management**: Clear separation of quiz data and user responses

## Future Expansion Guidelines

**When adding new NIOS lessons:**
1. Create corresponding text file with source material
2. Generate comprehensive MCQ JSON following established patterns
3. Update dropdown with new topic option
4. Ensure consistent naming and numbering
5. Test thoroughly before deployment

**Expected workflow for new content:**
- User provides text file with lesson content
- AI analyzes content and generates 40-50 MCQs
- AI creates JSON file with proper structure
- AI updates HTML dropdown if needed
- System ready for immediate use