# Copilot Instructions

## Project Overview

This is an educational web application for **NIOS Class 12 Interactive Learning Hub** featuring multiple subjects with MCQ quiz systems. It provides subject-specific quiz applications with dropdown-based topic selection that dynamically loads questions from JSON files and provides immediate feedback with explanations.

## Architecture

### Project Structure
```
NIOS/
├── index.html                    # Main kawaii landing page
├── cs/                          # Computer Science subject folder
│   ├── index.html              # CS quiz application
│   ├── cs.txt                  # Source material for CS topics
│   └── *.json                  # Individual topic MCQ databases
└── physics/                     # Physics subject folder
    ├── index.html              # Physics quiz application
    ├── physics.txt             # Source material for physics topics
    └── *.json                  # Individual topic MCQ databases (to be added)
```

### Core Components
- **Root `index.html`** - Kawaii-styled landing page with subject selection
- **Subject-specific `index.html`** - Complete SPA with embedded CSS/JS and dropdown selector
- **Subject text files** - Source educational content (`cs.txt`, `physics.txt`)
- **MCQ JSON files** - Question databases organized by topics within subject folders

### Data Flow
```
Landing Page → Subject Selection → Quiz Selector Dropdown → JSON File Selection → Fetch API → Dynamic DOM → User Interaction → Score Calculation
```

## Navigation Structure

### Main Landing Page (`/index.html`)
- **Purpose**: Kawaii-styled subject selection hub
- **Features**: 
  - Animated subject cards with hover effects
  - Responsive grid layout for multiple subjects
  - Direct navigation to subject-specific quiz apps
  - Progress indicators and feature highlights

### Subject-Specific Applications
- **Computer Science** (`/cs/index.html`): C++ programming topics with 16 MCQ modules
- **Physics** (`/physics/index.html`): Physics concepts and principles (expandable)
- **Future Subjects**: Easy to add new subject folders following the same pattern

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

### Creating New MCQ JSON Files from Subject Text Files

**When given a subject text file (cs.txt, physics.txt, etc.):**

1. **Analyze Source Material**
   - Read the entire subject text file to understand topics covered
   - Identify key concepts, definitions, formulas, principles, etc.
   - Note NIOS lesson numbers and module information
   - Understand subject-specific terminology and concepts

2. **Generate Comprehensive MCQs**
   - Create 40-50 questions per topic covering all major concepts
   - Follow the established JSON schema exactly
   - Ensure sequential numbering starting from 1
   - Use 0-indexed correctAnswer values
   - Adapt question types to subject requirements

3. **Subject-Specific Question Types**

   **For Computer Science (C++/Programming):**
   - **Conceptual**: "What is...?", "Which statement is true...?"
   - **Functional**: "What does function X do?", "Which header file...?"
   - **Syntax**: "How do you declare...?", "What symbol is used...?"
   - **Comparative**: "What is the difference between...?"
   - **Applied**: Code output questions, parameter passing scenarios

   **For Physics:**
   - **Conceptual**: Laws, principles, and theoretical understanding
   - **Formula-based**: Calculations and mathematical applications
   - **Unit/Measurement**: SI units, conversions, dimensional analysis
   - **Experimental**: Lab procedures, observations, conclusions
   - **Applied**: Real-world physics applications and problem-solving

   **For Other Subjects:**
   - Adapt question types based on subject methodology
   - Maintain educational rigor and curriculum alignment
   - Include both theoretical and practical applications

4. **MCQ Quality Standards**
   - Clear, unambiguous question stems
   - Four distinct options (A, B, C, D)
   - One clearly correct answer
   - Detailed explanations for educational value
   - Cover both basic and advanced concepts

5. **File Naming Convention**
   - Format: `{Topic}_MCQ.json`
   - Examples: `Functions_MCQ.json`, `Arrays_MCQ.json`, `Mechanics_MCQ.json`
   - Place files in appropriate subject folder (`/cs/`, `/physics/`, etc.)

6. **Update Subject HTML Dropdown**
   - Add new option to quiz selector dropdown in subject's index.html
   - Use descriptive names: "Topic Name (Lesson X)"
   - Maintain lesson number order for educational flow

### Adding New Questions to Existing Files
1. Add to appropriate JSON file following schema
2. Ensure sequential IDs and 0-indexed `correctAnswer`
3. Test explanation rendering and answer feedback

### UI Modifications
- All styling is embedded in `<style>` section of each HTML file
- JavaScript functions handle dynamic loading in subject-specific apps
- Gradient themes: Computer Science uses blue-purple, Physics uses warm colors
- Responsive design for mobile devices
- Kawaii landing page with animated subject cards

### Testing Locally
- Serve via local HTTP server (required for fetch API)
- Common: `python -m http.server 8000` or Live Server extension
- Access: `http://localhost:8000`
- Test dropdown functionality and JSON loading

### Educational Content Context

### Current Subjects Available

#### Computer Science (`/cs/`)
- **Source Material**: `cs.txt` - NIOS Class 12 Computer Science curriculum
- **Available Topics** (16 MCQ modules):
  - **Lesson 14**: Control Statements (if, switch, loops, jumps)
  - **Lesson 15**: Functions (library functions, user-defined, parameters, scope)
  - Arrays, Pointers, File Handling, Classes & Objects
  - Database Management, Web Designing, Operating Systems
  - Data Communication, Networking, and more
- **Question Coverage**: 600+ comprehensive MCQs across all topics

#### Physics (`/physics/`)
- **Source Material**: `physics.txt` - NIOS Class 12 Physics curriculum  
- **Status**: Framework ready, MCQ content to be developed
- **Planned Topics**: Mechanics, Thermodynamics, Optics, Modern Physics
- **Future Implementation**: Following same JSON structure as CS module

### Content Sources
- NIOS Class 12 official curriculum materials
- Subject-specific text files containing comprehensive lesson content
- Official NIOS modules and educational standards

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