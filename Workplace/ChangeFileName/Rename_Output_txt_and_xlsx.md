> REMEMBER TO CHANGE "folder_path" BEFORE RUNNING THE PROJECT  
> 运行前注意修改folder_path!!!
```python
import os
import csv
import pandas as pd

# 指定文件夹路径
folder_path = input('path: ') or r"C:\Users\荒酱\Documents\TF卡文件处理中站\第一次压缩"

# 获取文件夹下的所有文件
files = os.listdir(folder_path)

# 定义输出结果的txt文件路径
output_txt_file_path = os.path.join(folder_path, 'file_rename_results.txt')

# 定义输出结果的Excel文件路径
output_excel_file_path = os.path.join(folder_path, 'file_rename_results.xlsx')

# 遍历文件并重命名
with open(output_txt_file_path, 'w') as output_txt_file, open(output_excel_file_path, 'w',
                                                              newline='') as output_excel_file:
    txt_writer = csv.writer(output_txt_file, delimiter='\t')  # 使用制表符作为分隔符

    # 写入表头
    txt_writer.writerow(["Index", "Original File Name", "File Extension"])

    # 创建一个DataFrame用于保存结果
    df = pd.DataFrame(columns=["Index", "Original File Name", "File Extension"])

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
        result_line = f"{index + 1} --> {file_name[:]}\t{file_extension}\n"
        output_txt_file.write(result_line)

        print(f"ready for {index + 1} --> {file_name[0:10]}***{file_extension}")
        # 同时将结果添加到DataFrame中
        df = pd.concat([df, pd.DataFrame(
            {"Index": [index + 1], "Original File Name": [file_name], "File Extension": [file_extension]})],
                       ignore_index=True)
    # 将DataFrame写入Excel文件
    df.to_excel(output_excel_file_path, index=False)

# 输出完成提示
print(f"重命名结果已写入：\n- {output_txt_file_path}\n- {output_excel_file_path}")
