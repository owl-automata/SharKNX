# How to Report an Issue

Thank you for helping us improve SharKNX! Detailed bug reports help us fix problems faster. Please follow this guide to report issues effectively.

## Before You Report

- **Check existing issues** - Search [GitHub Issues](https://github.com/your-org/SharKNX/issues) to see if your issue already exists
- **Try troubleshooting** - See our [Troubleshooting Guide](../docs/troubleshooting.md) for common solutions
- **Update the app** - Make sure you're using the latest version from Google Play or App Store

## How to Report

### Via GitHub Issues (Recommended for Technical Issues)

1. Click **"New Issue"** on the [GitHub Issues page](https://github.com/your-org/SharKNX/issues)
2. Fill out all fields in the template below
3. Submit and monitor for follow-up questions

### Via Email (General Support)

Send a detailed report to **info@owl-automata.com** with the subject line: `[Bug Report] Brief description`

---

## Bug Report Template

Use this template when reporting bugs. The more details you provide, the faster we can help!

```
## App Information
- **SharKNX Version**: [e.g., 1.2.0+15]
- **Platform**: [Android / iOS]
- **Device Model**: [e.g., Samsung Galaxy A12, iPhone 14]
- **OS Version**: [e.g., Android 12, iOS 15.2]

## Bug Description
[Clear, concise description of the bug]

## Steps to Reproduce
1. [First step]
2. [Second step]
3. [Continue as needed...]

## Expected Behavior
[What should happen]

## Actual Behavior
[What actually happens]

## Screenshots / Logs (Optional)
[Attach screenshots or error logs if relevant]

## Additional Context
[Any other information that might help, e.g., network conditions, gateway type, etc.]
```

---

## Example Bug Report

```
## App Information
- **SharKNX Version**: 1.2.0+15
- **Platform**: Android
- **Device Model**: Samsung Galaxy A12
- **OS Version**: Android 11

## Bug Description
App crashes when importing a .knxproj file larger than 5MB

## Steps to Reproduce
1. Launch SharKNX
2. Go to "ETS Project Viewer"
3. Select "Import Project"
4. Choose a .knxproj file (6MB+)
5. Tap "Open"

## Expected Behavior
Project imports successfully and displays building structure

## Actual Behavior
App crashes immediately with error message "someErrorMessage"

## Screenshots / Logs
[Screenshot of crash message attached]

## Additional Context
- Using KNXnet/IP Tunneling mode
- Gateway: Weinzierl KNX IP BAOS
```

---

## Best Practices

**DO:**
- Be specific and detailed
- Include your exact app version and device info
- Describe steps so we can reproduce the issue
- Attach screenshots when relevant
- Check if the issue happens consistently or intermittently
- Be respectful and patient

**DON'T:**
- Report vague issues like "it doesn't work"
- Report the same issue multiple times
- Use multiple issues for the same problem

---

## What Happens Next?

1. **Acknowledgment** - We'll review your report within 2-3 business days
2. **Investigation** - We may ask follow-up questions
3. **Fix or Workaround** - We'll either fix the bug or provide a workaround
4. **Update** - You'll be notified when your issue is resolved

---

## Need Immediate Help?

For urgent issues or general support, email us at **info@owl-automata.com** with:
- Your issue description
- Screenshots if available
- Preferred contact method and best time to reach you
