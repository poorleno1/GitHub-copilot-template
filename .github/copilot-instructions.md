# GitHub Copilot Instructions

You are assisting a developer working on infrastructure automation projects using Terraform and PowerShell. Follow these global guidelines:

## General Code Quality

- Write clean, readable, and maintainable code
- Follow industry best practices and conventions
- Include comprehensive comments explaining complex logic
- Use meaningful variable and function names
- Implement proper error handling and validation

## Documentation Standards

- Always include docstrings/help comments for functions and modules
- Add inline comments for complex logic
- Create README files for new projects or major components
- Document prerequisites, dependencies, and setup instructions

## README File Requirements

Every project should include a README.md with the following sections:

- **Project Title and Description**: Clear, concise explanation of what the project does
- **Prerequisites**: Required tools, versions, and dependencies
- **Installation/Setup**: Step-by-step instructions to get started
- **Usage**: Examples of how to use the project
- **Configuration**: Environment variables, settings, and customization options
- **Contributing**: Guidelines for contributors (if applicable)
- **License**: License information
- **Contact/Support**: How to get help or report issues

## Security Best Practices

- Never hardcode sensitive information (passwords, API keys, etc.)
- Use environment variables or secure key management systems
- Follow the principle of least privilege
- Implement input validation and sanitization
- Use secure communication protocols

## Version Control

- Write descriptive commit messages
- Follow conventional commit format when possible
- Keep commits focused and atomic
- Include relevant issue references

## Testing and Validation

- Include unit tests where applicable
- Validate configurations before deployment
- Use linting tools and formatters
- Test in non-production environments first

## Project Structure

- Maintain consistent directory structure
- Separate concerns appropriately
- Use modular design patterns
- Keep configuration files organized and documented
