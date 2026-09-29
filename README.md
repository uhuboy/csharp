# Enterprise User Management System (C# WinForms)

A robust, enterprise-grade desktop application built using **C# Windows Forms (.NET)**. This project demonstrates best practices in WinForms development, including Object-Oriented Programming (OOP) principles, structured data binding, comprehensive input validation, and clean separation of concerns.

---

## 🚀 Features

*   **Interactive GUI:** Built with Windows Forms leveraging responsive layout containers.
*   **Dynamic Data Binding:** Utilizes `BindingList<T>` to automatically synchronize user additions/removals with a `DataGridView` UI component.
*   **Robust Input Validation:** Implements strict type checking (`int.TryParse`), range validation, and sanitization for user inputs to prevent crashes.
*   **Structured Data Modeling:** Encapsulates business data using clean, reusable object-oriented classes (`UserProfile`).
*   **User-Friendly Feedback:** Provides dynamic status updates and error handling dialog boxes (`MessageBox`).

---

## 📂 Project Architecture

The application follows standard WinForms modular organization:
```text
EnterpriseWinFormsApp/
│
├── Program.cs             # Application entry point (Main method & UI configuration)
├── MainForm.cs            # Code-behind logic, event handlers, and data processing
├── MainForm.Designer.cs   # Auto-generated UI layout code and control instantiations
└── UserProfile.cs         # Data model representing individual user entities
```

---

## 🛠️ Prerequisites & Requirements

*   **Operating System:** Windows 7 / 8 / 10 / 11
*   **Runtime/SDK:** .NET Framework (4.5 or higher) or .NET Core/.NET 6+ (depending on target project configuration)
*   **IDE:** Visual Studio 2019 / 2022 (with the *Desktop development with C#* workload installed)

---

## ⚙️ Getting Started & Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/enterprise-winforms-app.git
    ```
2.  **Open the project:**
    Open the solution file (`.sln`) in **Visual Studio**.
3.  **Build the solution:**
    Press `Ctrl + Shift + B` or navigate to `Build > Build Solution` to restore dependencies and compile code.
4.  **Run the application:**
    Press `F5` or click the **Start** button in Visual Studio to launch the desktop application.

---

## 💡 Core Code Snippet (`MainForm.cs`)

Here is a sample of how data validation and dynamic binding are handled within the application controller:

```csharp
private void btnSubmit_Click(object sender, EventArgs e)
{
    try
    {
        string name = txtName.Text.Trim();
        string role = comboBoxRole.SelectedItem.ToString();

        // Validate name input
        if (string.IsNullOrEmpty(name))
        {
            MessageBox.Show("Validation Error: Name cannot be empty.", "Error", MessageBoxButtons.OK, MessageBoxIcon.Warning);
            return;
        }

        // Safe integer parsing and range validation
        if (!int.TryParse(txtAge.Text.Trim(), out int age) || age <= 0 || age > 120)
        {
            MessageBox.Show("Validation Error: Enter a valid age between 1 and 120.", "Error", MessageBoxButtons.OK, MessageBoxIcon.Warning);
            return;
        }

        // Add to data-bound list
        UserProfile newUser = new UserProfile(name, age, role);
        _userList.Add(newUser);

        ClearFormInputs();
        lblStatus.Text = $"Success: Added user '{name}'.";
    }
    catch (Exception ex)
    {
        MessageBox.Show($"An unexpected error occurred: {ex.Message}", "Critical Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
    }
}
```

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
