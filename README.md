import pandas as pd
import tkinter as tk
from tkinter import messagebox, simpledialog, ttk
import os

# File CSV
data_file = 'abc.csv'

def load_data():
    if os.path.exists(data_file):
        return pd.read_csv(data_file)
    else:
        return pd.DataFrame(columns=['ID', 'Name', 'Age', 'Overall_Rating'])

def save_data():
    data.to_csv(data_file, index=False)
    refresh_table()

def refresh_table():
    for row in table.get_children():
        table.delete(row)
    for index, row in data.iterrows():
        table.insert("", "end", values=list(row))

def add_entry():
    global data
    new_entry = {}
    for col in data.columns:
        value = simpledialog.askstring("Input", f"Enter value for {col}:", parent=root)
        if value is None:
            return
        new_entry[col] = value
    data = pd.concat([data, pd.DataFrame([new_entry])], ignore_index=True)
    save_data()
    messagebox.showinfo("Success", "Entry added successfully!")

def delete_entry():
    global data
    selected_item = table.selection()
    if not selected_item:
        messagebox.showerror("Error", "Please select a row to delete")
        return
    index = table.index(selected_item)
    data = data.drop(index).reset_index(drop=True)
    save_data()
    messagebox.showinfo("Success", "Entry deleted successfully!")

def update_entry():
    global data
    selected_item = table.selection()
    if not selected_item:
        messagebox.showerror("Error", "Please select a row to update")
        return
    index = table.index(selected_item)
    for col in data.columns:
        value = simpledialog.askstring("Input", f"Enter new value for {col} (leave blank to keep current):", parent=root)
        if value:
            data.at[index, col] = value
    save_data()
    messagebox.showinfo("Success", "Entry updated successfully!")

def exit_program():
    root.destroy()


data = load_data()
root = tk.Tk()
root.title("CRUD Application with Tkinter and Pandas")
root.geometry("800x400")


table_frame = tk.Frame(root)
table_frame.pack(fill=tk.BOTH, expand=True)

columns = list(data.columns)
table = ttk.Treeview(table_frame, columns=columns, show='headings')
for col in columns:
    table.heading(col, text=col)
    table.column(col, width=100)

table.pack(fill=tk.BOTH, expand=True)
refresh_table()


button_frame = tk.Frame(root)
button_frame.pack(fill=tk.X)

tk.Button(button_frame, text="Add Entry", command=add_entry).pack(side=tk.LEFT, padx=10, pady=10)
tk.Button(button_frame, text="Update Entry", command=update_entry).pack(side=tk.LEFT, padx=10, pady=10)
tk.Button(button_frame, text="Delete Entry", command=delete_entry).pack(side=tk.LEFT, padx=10, pady=10)
tk.Button(button_frame, text="Exit", command=exit_program).pack(side=tk.RIGHT, padx=10, pady=10)

root.mainloop()



# BIEU DO CAN NANG

import pandas as pd
import matplotlib.pyplot as plt
# Đọc file CSV
data pd.read_csv('abc.csv')
# Vẽ biểu đồ histogram cân năng
plt.figure(figsize=(10, 6))
plt.hist(data['weight_kgs'], bins=15, color='lightgreen', edgecolor='black')
plt.title('Phân bố cân nặng cầu thủ')
plt.xlabel('Weight (kg)')
plt.ylabel('Số lượng câu thủ')
plt.grid(axis='y', linestyle'', alpha=0.7)
plt.show()



# BIEU DO CHIEU CAO
# Đọc dữ liệu từ file csv
data=pd.read_csv('abc.csv')
# Kiểm tra tên cột và dữ liệu
print(data.head))
# Giả sử cột chứa chiều cao tên là 'height_cm'
# Vẽ biểu đồ histogram
pet.figure(figsize=(10,6))
plt.hist(data['height_cm'], bins=15, color='skyblue', edgecolor='black')
plt.title('Phân bố chiều cao cầu thủ)
plt.xlabel('Height (cm)')
plt.ylabel('Số lượng cầu thủ')
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()




# BIEU DO COT
# Đọc dữ liệu từ file mới
file_path = "abc.csv"
data pd.read_csv(file_path)
# Xử lý dữ liệu: Loại bỏ các giá trị thiếu trong cột value_euro
data_cleaned = data.dropna (subset=['value_euro'])
# Nhóm theo quốc gia và tỉnh tổng value_euro, sau đó lấy top 15 quốc gia
top_15_countries = (
data_cleaned.groupby('nationality') ['value_euro']
.sum()
.sort_values(ascending=False)
.head (15)
5
)
# Vẽ biểu đồ cột cho top 15 quốc gia
import matplotlib.pyplot as plt
plt.figure(figsize=(12, 6))
top_15_countries.plot(kind='bar', color='skyblue', edgecolor='black')
plt.title(label: Top 15 Quốc gia có tổng giá trị cầu thủ (value_euro) cao nhất', fontsize=14)
plt.xlabel(xlabel: 'Quốc gia', fontsize=12)
plt.ylabel(ylabel: 'Tổng giá trị (value_euro)', fontsize=12)
plt.xticks(rotation=45)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.tight_layout()
plt.show()



# BIEU DO TRON
# Đọc dữ liệu từ file
file_path = "abc.csv" # Thay bằng đường dẫn tới file của bạn
data pd.read_csv(file_path)
# Đếm số lượng cầu thủ theo quốc gia
player_distribution = data['nationality'].value_counts()
# Lựa chọn hiển thị top 10 quốc gia, các quốc gia còn lại gộp vào "Others"
top_countries player_distribution.head(10)
others player_distribution.iloc[10:].sum()
top_countries ['Others'] = others
# Vẽ biểu đồ tròn
plt.figure(figsize=(8, 8))
top_countries.plot(kind='pie', autopct='%1.1f%%', startangle=90, colors=plt.cm.tab10.colors)
plt.title(label: 'Phân bố cầu thủ theo quốc gia, fontsize=14)
plt.ylabel('') # Xóa nhăn Y
plt.tight_layout()
plt.show()





# BIEU DO TUOI
# Đọc file CSV
df pd.read_csv('abc.csv')
# Giả sử cột chứa tuổi có tên là 'age'
# Kiểm tra tên các cột để chắc chắn
print(df.columns)
# Vẽ biểu đồ histogram cho cột 'age'
plt.figure(figsize=(8, 5))
plt.hist(df ['age'], bins=15, color="teal', edgecolor='black')
# Thiết lập tiêu đề và nhân
plt.title('Phân bố độ tuổi cầu thủ')
plt.xlabel('Age')
plt.ylabel('Số lượng cầu thủ')
# Hiển thị biểu đồ
plt.show()



# TRUC QUAN HOA
data=pd.read_csv('abc.csv')
# Nhóm dữ liệu theo nationality và tính điểm trung binh của overall_rating
rating_by_nationality data.groupby('nationality') ['overall_rating'].mean().sort_values(ascending=False).head(10)
# Vẽ biểu đồ cột
plt.figure(figsize=(10, 6))
rating_by_nationality.plot(kind='bar', color='skyblue', edgecolor='black')
plt.title(label: So sánh Overall Rating trung bình theo Quốc tịch (Top 10)', fontsize=14)
plt.xlabel(xlabel: 'Quốc tịch', fontsize=12)
plt.ylabel(ylabel: 'Overall Rating trung bình', fontsize=12)
plt.xticks (rotation=45)
plt.grid(axis='y', linestyle'', alpha=0.7)
plt.tight_layout()
plt.show()
