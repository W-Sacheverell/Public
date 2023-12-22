```python

import pandas as pd


def excel_to_markdown(excel_file_path, sheet_name):
    # 读取 Excel 文件
    df = pd.read_excel(excel_file_path, sheet_name=sheet_name)

    # 将数据转换为 Markdown 格式
    markdown_output = df.to_markdown(index=False)

    return markdown_output
```
An example is as follows, to print the result directly  
And the results were placed to following link:  
[Output.md](https://github.com/W-Sacheverell/W-Akaso/blob/main/WaitForRecovery/Output.md) 

```python
# 你的 Excel 文件路径和表格名称
excel_file_path = r"C:\Users\荒酱\OneDrive\文档\output - 副本 - 副本.xlsx"
sheet_names = ["1202", "1201", "1130"]  # 你的表格名称 例如为1202 1201 1130

for sheet_name in sheet_names:
    # 获取 Markdown 输出
    markdown_output = excel_to_markdown(excel_file_path, sheet_name)
    print("#", sheet_name)
    # 打印 Markdown 输出或将其保存到文件中，视需求而定
    print(markdown_output)
    print()
```
