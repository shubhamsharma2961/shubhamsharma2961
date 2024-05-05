import tkinter as tk
import pandas as pd

df = pd.read_csv("EPICS Bhopal.csv")

def accident_stats(Casualty_severity, Cause_of_accident, Accident_severity):
  filtered_df = df[
      (df['Casualty_severity'] == Casualty_severity) &
      (df['Cause_of_accident'] == Cause_of_accident) &
      (df['Accident_severity'] == Accident_severity)
  ]
  total_accidents = len(filtered_df)
  return total_accidents

def get_user_input():
  Casualty_severity = severity_var.get()
  Cause_of_accident = cause_var.get()
  Accident_severity = accident_var.get()
  return Casualty_severity, Cause_of_accident, Accident_severity

def show_results():
  Casualty_severity, Cause_of_accident, Accident_severity = get_user_input()
  total_accidents = accident_stats(Casualty_severity, Cause_of_accident, Accident_severity)
  result_label.config(text=f"Total accidents according to your input in this week: {total_accidents}")
    
root = tk.Tk()
root.title("Accident Statistics")

severity_label = tk.Label(root, text="Casualty severity:")
severity_label.pack()
severity_var = tk.StringVar(root)
severity_var.set("select")
severity_menu = tk.OptionMenu(root, severity_var, "na", "1", "2", "3", "4")
severity_menu.pack()

cause_label = tk.Label(root, text="Cause of accident:")
cause_label.pack()
cause_var = tk.StringVar(root)
cause_var.set("select")
cause_menu = tk.OptionMenu(root, cause_var, "Driving under the influence of drugs", "Moving Backward", "Changing lane to the left", "Changing lane to the right", "Overtaking")
cause_menu.pack()

accident_label = tk.Label(root, text="Accident severity:")
accident_label.pack()
accident_var = tk.StringVar(root)
accident_var.set("select")
accident_menu = tk.OptionMenu(root, accident_var, "Slight Injury", "Serious Injury")
accident_menu.pack()

submit_button = tk.Button(root, text="Submit", command=show_results)
submit_button.pack()

result_label = tk.Label(root)
result_label.pack()

root.mainloop()

