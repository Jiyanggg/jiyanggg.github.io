```
item = dict()
pattern_dict = {
    'project_name': re.compile(r'项目名称：(.*?)\n'),
    'project_funds': re.compile(r'预算投资总额：{0,1}\s{0,4}(.*)\n'),
    'project_end_date': re.compile(r'预计截止年月：{0,1}\s{0,4}(.*)\n'),
}

for field, pattern in pattern_dict.items():
    result = re.search(pattern=pattern, string=content)
    item[field] = result.group(1) if result else ''
print(item)