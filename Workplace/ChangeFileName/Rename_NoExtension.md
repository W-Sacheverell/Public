```python
import os

# 指定文件夹路径
folder_path = r"C:\Users\荒酱\AppData\Roaming\JetBrains\PyCharmCE2023.2\scratches\更改文件名称\新建文件夹"

# 获取文件夹下的所有文件
files = os.listdir(folder_path)

# 定义输出结果的txt文件路径
output_file_path = os.path.join(folder_path, 'file_rename_results.txt')

# 遍历文件并重命名
with open(output_file_path, 'w') as output_file:
    for index, file_name in enumerate(files):
        # 获取文件扩展名
        _, file_extension = os.path.splitext(file_name)

        # 构造新文件名（去除扩展名）
        new_name = f"{index + 1}"

        # 构造旧文件路径和新文件路径
        old_path = os.path.join(folder_path, file_name)
        new_path = os.path.join(folder_path, new_name)

        # 重命名文件
        os.rename(old_path, new_path)

        # 输出修改结果到txt文件
        result_line = f"{index + 1}--> {file_name}\n"
        output_file.write(result_line)

# 输出完成提示
print(f"重命名结果已写入：{output_file_path}")
