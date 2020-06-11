# coding: utf-8
with open('report.txt','r',encoding='utf-8') as f:
    lst1 = f.readlines()
    #print('lst1:', lst1)
    f.close()

score = []  #设置一个成绩的空列表
for line in lst1:
    line = line.split()
    score.append(line)

score[0].insert(0,'名次')
score[0].extend(['总分','平均分'])
#print(score)

for i in score[1:]:  #对嵌套的列表进行遍历
    #print(i)
    sum = 0
    avg = 0
    for j in i[1:]:  #对每人的成绩进行遍历
        #print(j)
        sum += float(j)   #计算每个人的总成绩
    #print(sum)
    avg = round(sum/len(i[1:]),1)  #计算每个人的平均分
    #print('len(i[1:]):',len(i[1:]))
    #print(avg)
    i.append(str(sum)) #为了便于后面排序，把得到总分再转化为字符
    i.append(str(avg))  #为了便于后面排序，把得到平均分再转化为字符
    #print('i',i)

    #对学生成绩按总分进行排序。使用sort函数排序，其中用lambda指定排序项为第11列的总分，用reverse指定是否要降序排列。
score.sort(key = lambda x:x[11],reverse = True)
for num in range(1,len(score)):   #给排列好的列表加上名次序号
    score[num].insert(0,num)
#print('score:',score)

#将排序后结果打印到屏幕上。通过for函数遍历每行、每列，并在每行结束后打印一个换行，这样效果会更好。
for h in score: #遍历行
    for k in range(13): #遍历一行中的每一列
        print(h[k],end = '\t')
    print()

#计算每科的平均成绩并替换60分以下的分数为不及格
lst_avg = ['0','平均']
for l in range(2,13):
    sum = 0
    for m in range(1,len(score)):
        sum += float(score[m][l])
        if float(score[m][l]) < 60:
            score[m][l] = '不及格'
        ave = round(sum / (len(score)-1),1)
    lst_avg.append(ave)
    #print(lst_avg)

score.insert(1,lst_avg)
#print(score)

for i in score:
    for j in range(13):
        print(i[j],end = '\t')
    print()

with open ('result.txt','w',encoding = 'utf-8') as f1:
    for h in score:
        for i in h:
            f1.write(str(i)+'\t')
        f1.write('\n')
