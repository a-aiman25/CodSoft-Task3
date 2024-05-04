# CodSoft-To-Do-List
Create a to-do list application with Python's Tkinter library, allowing users to add, remove, and mark tasks as complete, all presented in an intuitive and visually appealing interface.

# Create To-Do List

import tkinter as tk
import tkinter.messagebox as messagebox

root = tk.Tk()
root.configure(background = "#7E9680")
root.title("To-Do App")
root.geometry("800x400")

tasks_list = []
counter = 1

def inputError():
    if entry.get() == "":
        messagebox.showerror("Input Error", "Please enter a task.")
        return 0
    return 1

def clear_taskNumberField():
    taskNumberField.delete(0.0, tk.END)

def clear_taskField():
    entry.delete(0, tk.END)

def insertTask():
    global counter
    value = inputError()
    if value == 0:
        return
    content = entry.get() + "\n"
    tasks_list.append(content)
    task_listbox.insert(tk.END, f"[{counter}]  {content}")
    counter += 1
    clear_taskField()

def delete():
    selected_task_index = task_listbox.curselection()
    if selected_task_index:
        del tasks_list[selected_task_index[0]]
        task_listbox.delete(selected_task_index[0])
        
def mark_done():
    selected_task_index = task_listbox.curselection()
    if selected_task_index:
        task_text = task_listbox.get(selected_task_index[0])
        new_task_text = task_text.replace(" [pending]", "[completed]").replace("\n", "\n    (Completed) ")
        task_listbox.delete(selected_task_index[0])
        task_listbox.insert(selected_task_index[0], new_task_text)

label1 = tk.Label(root, text = "TO - DO LIST", bg = "#7E9680", font = ("Elephant", 20, "underline"))
label1.place(x = 90, y = 50)

label2 = tk.Label(root, text = "Enter Your Task", bg = "#7E9680", font = ("Segoe UI Black", 17))
label2.place(x = 110, y = 120)

entry = tk.Entry(root, font = ("Calibri", 12), width = 35)
entry.place(x = 55, y = 165)

taskNumber = tk.Label(root, text = "Delete Task Number", bg = "#7E9680")
taskNumber.place()

taskNumberField = tk.Text(root, height = 1, width = 2, font = ("lucida", 11, "bold"))
taskNumberField.place()

submit_button = tk.Button(root, text = "Submit Task", fg = "Black", bg = "#E8DDC9", font = ("Seoge UI", 11, "bold"), padx = 50, command = insertTask)
submit_button.place(x = 100, y = 210)

delete_button = tk.Button(root, text = "Delete Task", fg = "Black", bg = "grey", font = ("Seoge UI", 10, "bold"), padx = 30, command = lambda: delete())
delete_button.place(x = 130, y = 288)

done_button = tk.Button(root, text = "Mark as Done", fg = "Black", bg = "grey", font = ("Seoge UI", 10, "bold"), padx = 30, command = lambda: mark_done())
done_button.place(x = 124, y = 250)

exit_button = tk.Button(root, text = "Exit", fg = "Black", bg = "#B22222", font = ("Seoge UI", 10, "bold"), padx = 30, command = exit)
exit_button.place(x = 155, y = 325)

task_listbox = tk.Listbox(root, height = 22, width = 65)
task_listbox.place(x = 380, y = 20)

root.mainloop()
