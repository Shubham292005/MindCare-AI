# Contributing to MindCare-AI 🧠💚

Thank you for your interest in contributing to MindCare-AI! We welcome contributions from developers, designers, mental health professionals, and community members.

## 📋 Code of Conduct

Please read and follow our [Code of Conduct](./CODE_OF_CONDUCT.md) to ensure a welcoming and inclusive community.

---

## 🚀 How to Contribute

### 1. **Report Bugs**
- Check if the bug already exists in [Issues](https://github.com/Shubham292005/MindCare-AI/issues)
- Include detailed information:
  - Steps to reproduce
  - Expected vs actual behavior
  - Screenshots/logs
  - Environment (OS, browser, version)

### 2. **Suggest Features**
- Open an issue with the `enhancement` label
- Clearly describe the feature and use case
- Consider how it aligns with our mission

### 3. **Submit Code**
- Fork the repository
- Create a feature branch: `git checkout -b feature/your-feature-name`
- Follow our coding standards
- Write tests for your code
- Submit a pull request with clear description

### 4. **Improve Documentation**
- Fix typos or unclear sections
- Add examples or clarifications
- Update API documentation
- Translate documentation

---

## 🛠️ Development Setup

### Prerequisites
```bash
Node.js 16+
Python 3.9+
PostgreSQL 13+
Redis 6+
Git
```

### Step-by-Step Setup

1. **Fork and Clone**
   ```bash
   git clone https://github.com/YOUR_USERNAME/MindCare-AI.git
   cd MindCare-AI
   ```

2. **Install Dependencies**
   ```bash
   npm install
   # For backend if using Python
   pip install -r requirements.txt
   ```

3. **Setup Environment**
   ```bash
   cp .env.example .env
   # Edit .env with your local configuration
   ```

4. **Setup Database**
   ```bash
   # Create PostgreSQL database
   createdb mindcare_ai_dev
   
   # Run migrations
   npm run migrate:dev
   
   # Seed test data
   npm run seed:dev
   ```

5. **Start Development Server**
   ```bash
   npm run dev
   # Application will be available at http://localhost:3000
   ```

---

## 📝 Coding Standards

### JavaScript/TypeScript
```typescript
// ✅ Good
const getUserMoodTrend = async (userId: string): Promise<MoodTrend> => {
  const moods = await Mood.find({ userId });
  return calculateTrend(moods);
};

// ❌ Avoid
async function get_user_mood_trend(userId) {
  // unclear variable names, no type safety
}
```

**Guidelines:**
- Use TypeScript for type safety
- Follow camelCase for variables/functions
- Use PascalCase for classes/components
- Add JSDoc comments for public functions
- Max line length: 100 characters
- Use arrow functions when possible

### Python
```python
# ✅ Good
def analyze_mood_sentiment(text: str) -> float:
    """
    Analyze sentiment of mood description.
    
    Args:
        text: User's mood description
        
    Returns:
        Sentiment score between 0 and 1
    """
    # implementation
```

**Guidelines:**
- Follow PEP 8 style guide
- Use type hints
- Add docstrings to all functions
- Use meaningful variable names

### React Components
```typescript
// ✅ Good Component
interface MoodTrackerProps {
  userId: string;
  onMoodUpdate: (mood: Mood) => void;
}

const MoodTracker: React.FC<MoodTrackerProps> = ({ userId, onMoodUpdate }) => {
  // implementation
};

export default MoodTracker;

// ❌ Avoid - Class components without memoization
class MoodTracker extends React.Component {
  // outdated approach
}
```

---

## ✅ Testing Requirements

### Unit Tests
```bash
npm run test
```

Requirements:
- 80%+ code coverage
- Test happy path and error cases
- Mock external dependencies
- Use Jest/Vitest

Example:
```typescript
describe('Mood Calculator', () => {
  it('should calculate average mood correctly', () => {
    const moods = [8, 7, 9];
    expect(calculateAverage(moods)).toBe(8);
  });

  it('should handle empty array', () => {
    expect(calculateAverage([])).toBe(0);
  });
});
```

### Integration Tests
```bash
npm run test:integration
```

Test database operations, API endpoints, external service calls.

### E2E Tests
```bash
npm run test:e2e
```

Test complete user flows using Cypress or Playwright.

---

## 🎯 Pull Request Process

1. **Update from Main**
   ```bash
   git fetch origin
   git rebase origin/main
   ```

2. **Write Clear Commit Messages**
   ```
   feat: Add mood prediction ML model
   
   - Implement LSTM model for mood prediction
   - Add training pipeline
   - Include unit tests
   
   Closes #123
   ```

3. **Push to Your Fork**
   ```bash
   git push origin feature/your-feature-name
   ```

4. **Create Pull Request**
   - Use the PR template
   - Link related issues
   - Describe changes clearly
   - Include screenshots for UI changes

5. **PR Review Checklist**
   - [ ] Code follows style guide
   - [ ] Tests added/updated
   - [ ] Documentation updated
   - [ ] No breaking changes (or noted)
   - [ ] Sensitive data not exposed
   - [ ] GDPR compliance maintained

6. **Address Review Comments**
   - Respond to all feedback
   - Push additional commits for changes
   - Don't force-push after review starts

---

## 🔄 Git Workflow

```
main (stable)
  ↑
  └─ staging (pre-production)
       ↑
       └─ feature/your-feature (your work)
```

**Branch Naming:**
- `feature/add-voice-interface`
- `fix/chatbot-crash-issue`
- `docs/update-readme`
- `refactor/optimize-queries`
- `test/add-crisis-detection-tests`

---

## 📚 Documentation Guidelines

### Code Documentation
```typescript
/**
 * Detects crisis indicators in user input
 * 
 * @param text - User's message to analyze
 * @param userId - User ID for context
 * @returns Crisis assessment with severity level
 * 
 * @example
 * const crisis = detectCrisis("I want to harm myself", userId);
 * if (crisis.severity > 0.8) notifyAdmin(userId);
 */
function detectCrisis(text: string, userId: string): CrisisAssessment {
  // implementation
}
```

### README Sections
- Problem statement
- Features
- Installation
- Usage
- API documentation
- Contributing
- License

### API Documentation
Use OpenAPI/Swagger format:
```yaml
/api/moods:
  post:
    summary: Log a new mood
    requestBody:
      required: true
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Mood'
    responses:
      201:
        description: Mood logged successfully
      400:
        description: Invalid input
```

---

## 🧪 Testing Mental Health Features

**Important:** When working on mental health features:
- Test with realistic crisis scenarios
- Ensure safety mechanisms work
- Validate helpline integration
- Test with diverse user personas
- Consider cultural sensitivity
- Get feedback from mental health professionals

---

## 📤 Submitting Your Work

### Before Final Submission
1. Run all tests locally
2. Check code quality with linter
3. Review your own PR first
4. Update documentation
5. Test in multiple browsers (if frontend)
6. Check mobile responsiveness

### PR Title Format
```
[type] Brief description

Types: feat, fix, docs, style, refactor, test, chore
Examples:
- feat: Add mood prediction using LSTM
- fix: Resolve chatbot crash in anonymous mode
- docs: Update API documentation
```

---

## 🐛 Debugging Tips

### Common Issues

**Database Connection Failed**
```bash
# Check PostgreSQL is running
psql -U postgres -d mindcare_ai_dev -c "SELECT 1;"

# Check Redis is running
redis-cli ping
```

**Port Already in Use**
```bash
# Find process using port 5000
lsof -i :5000
# Kill it
kill -9 <PID>
```

**Environment Variables Not Working**
```bash
# Ensure .env file exists
ls -la .env

# Check variables are loaded
npm run dev -- --debug
```

---

## 🚢 Deployment Testing

Before merging to main:
1. Test in staging environment
2. Run performance tests
3. Security scanning
4. Database migration tests
5. Backup/recovery testing

---

## 📞 Getting Help

- **Issues**: Ask questions in GitHub Issues
- **Discussions**: Use GitHub Discussions for longer conversations
- **Email**: contact@mindcare-ai.com (placeholder)
- **Discord**: [Join our Discord](link-to-discord) (if available)

---

## 🎉 Recognition

Contributors will be:
- Added to CONTRIBUTORS.md
- Mentioned in release notes
- Recognized on the website
- Invited to contributor discussions

---

## 📋 Checklist Before Submitting PR

- [ ] Code follows style guide
- [ ] Added/updated tests
- [ ] All tests passing locally
- [ ] Documentation updated
- [ ] No console errors/warnings
- [ ] No sensitive data in commits
- [ ] Commit messages are clear
- [ ] PR description is detailed
- [ ] No merge conflicts
- [ ] Linked related issues

---

## 🔐 Security Considerations

When contributing:
- **Never commit sensitive data** (API keys, passwords)
- Use `.env` for secrets
- Validate all user input
- Sanitize output for XSS prevention
- Use parameterized queries for SQL
- Encrypt sensitive data
- Follow OWASP guidelines
- Report security issues privately: [Security Policy](./SECURITY.md)

---

## 📜 License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

## 🙏 Thank You!

We appreciate every contribution, no matter the size. Together, we're building a safer, more supportive mental health platform for millions of Indians. 💚

**Made with ❤️ for mental health**
