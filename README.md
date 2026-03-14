# Productivity Dashboard

A minimal, vanilla JavaScript productivity dashboard with greeting widget, focus timer, task list, and quick links.

## Features

- **Greeting Widget**: Time-based greetings with live clock
- **Focus Timer**: Pomodoro-style timer (25 minutes default)
- **Task List**: Create, complete, and delete tasks
- **Quick Links**: Save frequently used links

## Technology Stack

- HTML5
- CSS3
- Vanilla JavaScript
- Local Storage API

## Testing the Greeting Widget

The greeting widget functions have been designed to be testable. You can test them manually using the browser console.

### Testing Instructions

1. Open `index.html` in your browser
2. Open the browser console (F12 or right-click → Inspect → Console)
3. Run the test commands below

### Test Cases

#### Time Formatting Tests (Requirements 1.3, 1.4)

```javascript
// Test midnight (00:00) - should display as 12:00 AM
getCurrentTime(new Date('2024-01-01T00:00:00')); // Expected: "12:00 AM"

// Test midnight with minutes (00:30)
getCurrentTime(new Date('2024-01-01T00:30:00')); // Expected: "12:30 AM"

// Test noon (12:00) - should display as 12:00 PM
getCurrentTime(new Date('2024-01-01T12:00:00')); // Expected: "12:00 PM"

// Test noon with minutes (12:45)
getCurrentTime(new Date('2024-01-01T12:45:00')); // Expected: "12:45 PM"

// Test early morning (1:00 AM)
getCurrentTime(new Date('2024-01-01T01:00:00')); // Expected: "1:00 AM"

// Test afternoon (3:45 PM / 15:45)
getCurrentTime(new Date('2024-01-01T15:45:00')); // Expected: "3:45 PM"

// Test single digit minutes with leading zero (3:05 AM)
getCurrentTime(new Date('2024-01-01T03:05:00')); // Expected: "3:05 AM"

// Test late night (11:59 PM / 23:59)
getCurrentTime(new Date('2024-01-01T23:59:00')); // Expected: "11:59 PM"
```

#### Greeting Message Tests (Requirement 1.5)

```javascript
// Good morning tests (5 AM - 11 AM)
getGreeting(new Date('2024-01-01T05:00:00')); // Expected: "Good morning"
getGreeting(new Date('2024-01-01T08:30:00')); // Expected: "Good morning"
getGreeting(new Date('2024-01-01T11:00:00')); // Expected: "Good morning"
getGreeting(new Date('2024-01-01T11:59:00')); // Expected: "Good morning"

// Good afternoon tests (12 PM - 4 PM)
getGreeting(new Date('2024-01-01T12:00:00')); // Expected: "Good afternoon"
getGreeting(new Date('2024-01-01T14:30:00')); // Expected: "Good afternoon"
getGreeting(new Date('2024-01-01T16:00:00')); // Expected: "Good afternoon"
getGreeting(new Date('2024-01-01T16:59:00')); // Expected: "Good afternoon"

// Good evening tests (5 PM - 8 PM)
getGreeting(new Date('2024-01-01T17:00:00')); // Expected: "Good evening"
getGreeting(new Date('2024-01-01T19:00:00')); // Expected: "Good evening"
getGreeting(new Date('2024-01-01T20:00:00')); // Expected: "Good evening"
getGreeting(new Date('2024-01-01T20:59:00')); // Expected: "Good evening"

// Good night tests (9 PM - 4 AM)
getGreeting(new Date('2024-01-01T21:00:00')); // Expected: "Good night"
getGreeting(new Date('2024-01-01T23:00:00')); // Expected: "Good night"
getGreeting(new Date('2024-01-01T00:00:00')); // Expected: "Good night"
getGreeting(new Date('2024-01-01T02:00:00')); // Expected: "Good night"
getGreeting(new Date('2024-01-01T04:00:00')); // Expected: "Good night"
getGreeting(new Date('2024-01-01T04:59:00')); // Expected: "Good night"
```

#### Date Formatting Tests (Requirement 1.6)

```javascript
// Test standard date
getCurrentDate(new Date('2024-01-01T12:00:00')); // Expected: "Monday, January 1, 2024"

// Test different month
getCurrentDate(new Date('2024-07-04T12:00:00')); // Expected: "Thursday, July 4, 2024"

// Test end of year
getCurrentDate(new Date('2024-12-31T12:00:00')); // Expected: "Tuesday, December 31, 2024"

// Test leap year date
getCurrentDate(new Date('2024-02-29T12:00:00')); // Expected: "Thursday, February 29, 2024"
```

### Automated Test Runner (Optional)

You can also run all tests at once by pasting this into the console:

```javascript
// Simple test runner
const tests = [
    // Time formatting tests
    { fn: () => getCurrentTime(new Date('2024-01-01T00:00:00')), expected: '12:00 AM', name: 'Midnight formats as 12:00 AM' },
    { fn: () => getCurrentTime(new Date('2024-01-01T12:00:00')), expected: '12:00 PM', name: 'Noon formats as 12:00 PM' },
    { fn: () => getCurrentTime(new Date('2024-01-01T15:45:00')), expected: '3:45 PM', name: 'Afternoon time formats correctly' },
    { fn: () => getCurrentTime(new Date('2024-01-01T03:05:00')), expected: '3:05 AM', name: 'Leading zero for minutes' },
    
    // Greeting tests
    { fn: () => getGreeting(new Date('2024-01-01T08:00:00')), expected: 'Good morning', name: '8 AM returns Good morning' },
    { fn: () => getGreeting(new Date('2024-01-01T14:00:00')), expected: 'Good afternoon', name: '2 PM returns Good afternoon' },
    { fn: () => getGreeting(new Date('2024-01-01T19:00:00')), expected: 'Good evening', name: '7 PM returns Good evening' },
    { fn: () => getGreeting(new Date('2024-01-01T23:00:00')), expected: 'Good night', name: '11 PM returns Good night' },
    
    // Date formatting tests
    { fn: () => getCurrentDate(new Date('2024-01-01T12:00:00')), expected: 'Monday, January 1, 2024', name: 'Date formats correctly' },
];

let passed = 0, failed = 0;
tests.forEach(test => {
    const result = test.fn();
    if (result === test.expected) {
        console.log(`✓ ${test.name}`);
        passed++;
    } else {
        console.error(`✗ ${test.name} - Expected: "${test.expected}", Got: "${result}"`);
        failed++;
    }
});
console.log(`\nResults: ${passed} passed, ${failed} failed out of ${tests.length} tests`);
```

## Project Structure

```
/
├── index.html          # Main HTML file
├── css/
│   └── styles.css      # Single stylesheet
└── js/
    └── app.js          # Single JavaScript file
```

## Development Standards

See `.kiro/steering/productivity-dashboard-standards.md` for complete development guidelines.