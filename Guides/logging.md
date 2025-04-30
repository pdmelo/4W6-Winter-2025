# 📜Logging and Code Documentation

## 1. **Importance of Logging**

Logging is crucial in a web application once it is deployed for several reasons:

### 🛠️**Troubleshooting and Debugging:**
   Logs help developers identify and understand errors or unexpected behaviour in the application.
   When issues occur in production, logs provide detailed information about:

  - ❓What happened
  - 🕒When it happened
  - 🧠Why it possibly happened

  This makes it much easier to diagnose and fix problems without needing to reproduce the issue manually.

### 📈 **Monitoring and Performance Tracking:**
   Logs allow developers and system administrators to monitor the server’s health and performance over time.
   By analysing logs, you can detect:

  - 🐢 Slow response times
  - 🚀 High traffic patterns
  - 🔒 Potential security threats

  This helps maintain the system's stability, security, and performance proactively.

## 2. **Viewing Logs**

Logs can usually be viewed:

- Directly in the terminal where the server is running
- In log files generated automatically by the application
- In external monitoring tools or dashboards (ex. Datadog, New Relic, AWS CloudWatch)

Example of a simple log output:

```bash
bashCopyEdit[2025-04-28T14:52:00Z] INFO: Server started on port 3000
[2025-04-28T14:53:10Z] ERROR: Database connection failed - timeout after 5000ms
```

> [!tip]
> Always make sure that **sensitive data** (like passwords or user personal information) is not accidentally logged.

## **Best Practices for Logging** ✅

- Use different log levels (`info`, `warn`, `error`, `debug`) appropriately.
- 🕰️ Include timestamps in logs.
- Structure logs in a consistent, readable format (JSON format is common for server logs).
- 🚫 Avoid excessive logging to prevent performance degradation.
- 👀 Review and monitor logs regularly, not just when problems occur.(Usually used when an application is deployed live)



## 3.  **Importance of Code Documentation** 🧾

Good code documentation is essential for any software project, for several reasons:

- **📖 Improves Readability:**
   Well-documented code helps others (and your future self) quickly understand what the code is doing and why certain decisions were made.
- 👋 **Simplifies Onboarding:**
   When new developers join a project, clear documentation allows them to get up to speed faster without needing constant explanations.
- **🔧 Facilitates Maintenance and Updates:**
   Over time, software needs to be updated, fixed, or improved. Documentation acts as a guide, making it easier to modify or expand the code safely.
- 🤝 **Promotes Collaboration:**
   Clear documentation ensures that team members can collaborate effectively without misunderstanding the purpose or behavior of the code.



### **How to Document Your Code** 📝

- **Write Clear Comments:**
   Add comments to explain *why* complex code exists, not just *what* it does.

  Example:

  ```ts
  // Calculate the discounted price based on user membership level
  const finalPrice = calculateDiscount(price, membershipLevel);
  ```

- **Use Docstrings for Functions and Classes:**
   Describe what a function or class does, its parameters, and its return value.

  Example (TypeScript/JSDoc style):

  ```ts
  /**
   * Calculates the final price after applying membership discount.
   * @param price - The original product price
   * @param membershipLevel - The user's membership level ('gold', 'silver', 'bronze')
   * @returns The final price after discount
   */
  function calculateDiscount(price: number, membershipLevel: string): number {
    // implementation
  }
  ```

- **Document Project Structure:**
   In the project’s README file, explain:

  - What the project does
  - How to install and run it
  - Project structure (folder/file organization)
  - How to run tests



## **Best Practices for Code Documentation** ✅

- ✍️ Be concise but clear — avoid long essays.
- 🔄 Keep documentation updated as code changes.
- 📚 Use consistent formatting (Markdown, JSDoc, etc.).
- 🚫 Avoid stating the obvious — focus on explaining *non-trivial* parts.
- 💬 Prefer examples — showing how to use a function is often better than describing it.
