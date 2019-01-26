* [1.如何查找出现频率最高的100个ip地址](#1-如何查找出现频率最高的100个ip地址)

# 1. 如何查找出现频率最高的100个ip地址
#cat access_log |cut -d ' ' -f 1 |sort |uniq -c | sort -nr | awk '{print $0 }' | head -n 10 |less
