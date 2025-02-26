# Tổng quan 

Chào mừng đến với project phân tích dữ liệu của tôi, nơi cung cấp một cái nhìn chi tiết về thị trường việc làm trong lĩnh vực dữ liệu trên toàn cầu. Dự án này không chỉ nhằm cung cấp những thông tin quan trọng về tình hình hiện tại của thị trường việc làm mà còn để thể hiện kỹ năng và sự tận tâm của tôi. 

Bằng cách sử dụng Python và các công cụ phân tích khác, tôi đã giải quyết thành công bốn câu hỏi quan trọng liên quan đến ngành Data. Hơn nữa, các kết quả cũng được thể hiện dưới dạng các biểu đồ để có thể giúp người xem dễ hình dung các thông tin hơn. 

*LƯU Ý* 
- Dữ liệu chính được lấy từ Khóa học Python của Luke Barousse
- Do dữ liệu tại Việt Nam hạn chế, phân tích của tôi sẽ tập trung chủ yếu vào thị trường việc làm tại Hoa Kỳ.
- Các kết quả được đưa ra dựa trên dữ liệu hiện có và có thể không phản ánh tình hình thực tế của thị trường. 

# Các câu hỏi trọng tâm 

Project này hướng tới trả lời các câu hỏi sau: 


1. Đâu là những kỹ năng được yêu cầu nhiều nhất cho ba vị trí phổ biến nhất trong lĩnh vực dữ liệu tại Hoa Kỳ?
2. Xu hướng của ba kỹ năng được yêu cầu nhất cho Data Analyst là gì?
3. Mức lương của sáu công việc phổ biến nhất tại Hoa Kỳ là bao nhiêu?
4. Những kỹ năng tối ưu nhất cho Data Analyst là gì?

# Các công cụ tôi dùng 

Để phân tích sâu về thị trường việc làm của Data Analyst, tôi đã sử dụng một số công cụ quan trọng:

- Python: Công cụ chính trong phân tích của tôi, giúp xử lý dữ liệu và truy xuất những thông tin quan trọng. Đặc biệt, tôi đã sử dụng các thư viện Python sau:
    - Pandas: Dùng để thao tác và phân tích dữ liệu.
    - Matplotlib: Dùng để trực quan hóa dữ liệu.
    - Seaborn: Tạo các biểu đồ trực quan phức tạp hơn.
- Visual Studio Code: Trình soạn thảo chính để viết và chạy các script Python. 
- Git & GitHub: Kiểm soát các phiên bản của project, đồng thời chia sẻ và gây dựng lên network tương tác cho cộng đồng. 
# Những gì tôi học được từ project này 

* **Áp dụng kiến thức lập trình vào Phân tích dữ liệu** 


Dự án này đã giúp tôi hiểu cách Python có thể được sử dụng để phân tích dữ liệu thực tế. Tôi đã áp dụng nhiều thư viện Python như Pandas, Matplotlib để làm sạch, xử lý và diễn giải dữ liệu, giúp phân tích trở nên sâu sắc và hiệu quả hơn. 

* **Tăng cường tư duy logic và kỹ năng phân tích** 

Làm việc trên dự án này yêu cầu tôi phải chia nhỏ các vấn đề phức tạp thành những bước nhỏ, dễ quản lý hơn. Tôi đã cải thiện khả năng tư duy phản biện, sửa lỗi và tối ưu hóa mã để có hiệu suất tốt hơn, qua đó nâng cao kỹ năng giải quyết vấn đề của mình. 

* **Thành thạo trình bày dữ liệu dưới các dạng biểu đồ** 

Tôi đã học cách sử dụng hiệu quả các thư viện trực quan hóa dữ liệu như Matplotlib và Seaborn để trình bày kết quả một cách rõ ràng và trực quan. Kỹ năng này rất quan trọng để truyền đạt thông tin, giúp việc ra quyết định dựa trên dữ liệu trở nên dễ tiếp cận và có tác động hơn.

# The project 

Sau đây là project của tôi 
## Load & dọn dẹp dữ liệu 

Tôi bắt đầu project bằng cách tải xuống các thư viện và dataset cần thiết. Sau đó, tôi 'dọn dẹp' các dữ liệu để có thể tối ưu hóa khả năng xử lý dữ liệu sau này. 

``` python 
#Import 
import ast
import pandas as pd
import seaborn as sns
from datasets import load_dataset
import matplotlib.pyplot as plt  

#Load datasets 
dataset = load_dataset('lukebarousse/data_jobs')
df = dataset['train'].to_pandas() 
``` 
Để thấy chi tiết hơn bước dọn dẹp dữ liệu, hãy truy cập [1_Skills_Demand.ipynb](1_Skills_Demand.ipynb) 

Sau khi nhập và load các dữ liệu, tôi bắt đầu sửa lại các cột dữ liệu sao cho đúng với format cần thiết. 

``` python 
# Data Cleanup
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
``` 

## 1. Đâu là những kỹ năng được yêu cầu nhiều nhất cho ba vị trí phổ biến nhất trong lĩnh vực dữ liệu tại Hoa Kỳ? 

### Phân tích sơ bộ 
Version chi tiết: [1_Skills_Demand.ipynb](1_Skills_Demand.ipynb) 

Để có thể tìm được 3 nghề dữ liệu phổ biến nhất ở Hoa Kỳ, trước hết tôi sàng lọc DataFrame để chỉ cho thấy những nghề ở Hoa Kỳ. 

``` python 
df_US = df[df['job_country'] == 'United States']
``` 

Để tìm 3 nghề dữ liệu phổ biến nhất, tôi đã viết code python như sau: 

``` python 
df_US['job_title_short'].value_counts()
``` 
Kết quả: 3 nghề dữ liệu phổ biến nhất là Data Analyst, Data Scientist và Data Engineer 

Tiếp theo, tôi xác định tần suất xuất hiện của từng kỹ năng trong các job postings bằng cách tính phần trăm—chia tổng số lần một kỹ năng được đề cập cho tổng số job postings. 

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>job_skills</th>
      <th>job_title_short</th>
      <th>skill_count</th>
      <th>job_count</th>
      <th>skill_perc</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>python</td>
      <td>Data Scientist</td>
      <td>42379</td>
      <td>58830</td>
      <td>72.036376</td>
    </tr>
    <tr>
      <th>1</th>
      <td>sql</td>
      <td>Data Analyst</td>
      <td>34452</td>
      <td>67816</td>
      <td>50.802171</td>
    </tr>
    <tr>
      <th>2</th>
      <td>sql</td>
      <td>Data Scientist</td>
      <td>30034</td>
      <td>58830</td>
      <td>51.052184</td>
    </tr>
    <tr>
      <th>3</th>
      <td>excel</td>
      <td>Data Analyst</td>
      <td>27519</td>
      <td>67816</td>
      <td>40.578919</td>
    </tr>
    <tr>
      <th>4</th>
      <td>r</td>
      <td>Data Scientist</td>
      <td>26022</td>
      <td>58830</td>
      <td>44.232534</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1865</th>
      <td>clojure</td>
      <td>Software Engineer</td>
      <td>1</td>
      <td>1814</td>
      <td>0.055127</td>
    </tr>
    <tr>
      <th>1866</th>
      <td>vb.net</td>
      <td>Senior Data Scientist</td>
      <td>1</td>
      <td>12946</td>
      <td>0.007724</td>
    </tr>
    <tr>
      <th>1867</th>
      <td>fortran</td>
      <td>Machine Learning Engineer</td>
      <td>1</td>
      <td>921</td>
      <td>0.108578</td>
    </tr>
    <tr>
      <th>1868</th>
      <td>planner</td>
      <td>Cloud Engineer</td>
      <td>1</td>
      <td>423</td>
      <td>0.236407</td>
    </tr>
    <tr>
      <th>1869</th>
      <td>nltk</td>
      <td>Senior Data Engineer</td>
      <td>1</td>
      <td>9289</td>
      <td>0.010765</td>
    </tr>
  </tbody>
</table>
<p>1870 rows × 5 columns</p>
</div> 

Cuối cùng, tôi sử dụng `seaborn` để lập đồ thị đường (line chart) cho dữ liệu trên 


``` python 
import seaborn as sns 

fig, ax = plt.subplots(3,1) 

for i,job in enumerate(job_roles):
    df_plot = df_total[df_total['job_title_short'] == job].head(5) 
    sns.barplot(df_plot,x='skill_perc',y='job_skills',hue='skill_perc',ax=ax[i]) 
    ax[i].set(title=job, ylabel='', xlabel='')
    ax[i].legend().set_visible(False)
    ax[i].set_xlim(0,80)
    
    # label the percentage on the bars
    for j, value in enumerate(df_plot['skill_perc']): 
        ax[i].text(value + 0.1, j, f'{value:.0f}%', va='center',fontsize=8) 

    if i != 2: 
        ax[i].xaxis.set_visible(False)

fig.suptitle('PERCENTAGE OF SKILLS REQUIRED IN 3 MOST POPULAR JOBS')

plt.tight_layout()
``` 
### Kết quả 

![1_Skills_Demand]([Images/1_Skills_Demand.png](https://github.com/Dunglaiminh/Python_project/blob/95f61594c4bd6622f120b30e7b2e6e1858b0dd6e/Images/1_Skills_Demand.png)) 

### Thông tin rút ra 

* **SQL là kỹ năng quan trọng cho mọi ngành nghề**

SQL là một kỹ năng nền tảng trong ngành dữ liệu, được yêu cầu nhiều nhất đối với Data Engineer (68%), tiếp theo là Data Analyst (51%) và Data Scientist (51%). Việc SQL được sử dụng rộng rãi trong cả ba vai trò nhấn mạnh tầm quan trọng của nó trong quản lý cơ sở dữ liệu, truy vấn dữ liệu và xử lý dữ liệu có cấu trúc. Thành thạo SQL là điều cần thiết đối với bất kỳ ai theo đuổi sự nghiệp trong lĩnh vực dữ liệu. 

* **Python chiếm ưu thế trong Data Science & Engineering**

Python là kỹ năng được yêu cầu nhiều nhất đối với 
Data Scientist (72%) và cũng rất quan trọng đối với Data Engineer (65%). Python đóng vai trò cốt lõi trong phân tích dữ liệu. Tuy nhiên, nhu cầu về Python đối với Data Analyst thấp hơn đáng kể (27%), cho thấy rằng các nhà phân tích thường dựa vào các công cụ khác để xử lý dữ liệu và báo cáo hơn là lập trình chuyên sâu. 

* **Data Analyst phụ thuộc vào các công cụ Business Intelligence** 

Khác với Data Scientist và Data Engineer, Data Analyst chủ yếu sử dụng các công cụ Business Intelligence như Excel (41%) và Tableau (28%) để phân tích và trực quan hóa dữ liệu. Vai trò của họ tập trung nhiều hơn vào việc rút trích thông tin và trình bày kết quả thay vì xây dựng các mô hình phức tạp hoặc xử lý dữ liệu quy mô lớn. Điều này nhấn mạnh tầm quan trọng của kỹ năng trực quan hóa và truyền đạt thông tin trong vai trò của một Data Analyst. 

## 2. Xu hướng của ba kỹ năng được yêu cầu nhất cho Data Analyst là gì? 

### Phân tích sơ bộ
Version chi tiết:  [2_Skills_Trend.ipynb](2_Skills_Trend.ipynb) 

Trong phân tích này, tôi sẽ tập trung phần lớn vào nghề 'Data Analyst' trong Hoa Kỳ để có một nguồn dữ liệu phong phú hơn. 

```python 
#Filtering Data Analyst jobs in the United States 
df_US = df_exploded[(df_exploded['job_title_short'] == 'Data Analyst') & (df_exploded['job_country'] == 'United States')]
``` 

Tiếp theo, để tìm xu hướng của tất cả các kỹ năng, tôi sẽ tạo một pivot table đếm số lần mỗi kỹ năng xuất hiện hàng tháng bằng cách sử dụng `.pivot_table()`.

``` python 
#Creating a pivot table to track the number of skills posted each month.
df_pivot = df_US.pivot_table(index='job_posted_month',columns='job_skills',aggfunc='size',fill_value=0)
``` 

Đây là pivot table

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>job_skills</th>
      <th>sql</th>
      <th>excel</th>
      <th>tableau</th>
      <th>python</th>
      <th>sas</th>
    </tr>
    <tr>
      <th>job_posted_mon</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jan</th>
      <td>14.161716</td>
      <td>11.056050</td>
      <td>7.657977</td>
      <td>6.937733</td>
      <td>5.638832</td>
    </tr>
    <tr>
      <th>Feb</th>
      <td>13.657527</td>
      <td>11.152785</td>
      <td>7.225384</td>
      <td>6.975341</td>
      <td>5.225039</td>
    </tr>
    <tr>
      <th>Mar</th>
      <td>13.862748</td>
      <td>11.434833</td>
      <td>7.752138</td>
      <td>7.232177</td>
      <td>5.319926</td>
    </tr>
    <tr>
      <th>Apr</th>
      <td>13.813221</td>
      <td>10.934752</td>
      <td>7.674488</td>
      <td>7.202608</td>
      <td>5.585346</td>
    </tr>
    <tr>
      <th>May</th>
      <td>13.726533</td>
      <td>11.264160</td>
      <td>7.615806</td>
      <td>7.174387</td>
      <td>5.169388</td>
    </tr>
    <tr>
      <th>Jun</th>
      <td>13.362592</td>
      <td>11.121487</td>
      <td>7.601083</td>
      <td>7.512373</td>
      <td>4.594267</td>
    </tr>
    <tr>
      <th>Jul</th>
      <td>13.267901</td>
      <td>10.770952</td>
      <td>7.795972</td>
      <td>7.312856</td>
      <td>5.065094</td>
    </tr>
    <tr>
      <th>Aug</th>
      <td>13.325007</td>
      <td>10.659225</td>
      <td>7.614847</td>
      <td>7.903673</td>
      <td>4.980290</td>
    </tr>
    <tr>
      <th>Sep</th>
      <td>13.122534</td>
      <td>10.297902</td>
      <td>7.736291</td>
      <td>7.027274</td>
      <td>4.894505</td>
    </tr>
    <tr>
      <th>Oct</th>
      <td>13.470798</td>
      <td>10.058614</td>
      <td>7.478543</td>
      <td>7.185472</td>
      <td>5.024074</td>
    </tr>
    <tr>
      <th>Nov</th>
      <td>13.452974</td>
      <td>10.040608</td>
      <td>7.518994</td>
      <td>6.870579</td>
      <td>5.187320</td>
    </tr>
    <tr>
      <th>Dec</th>
      <td>12.613473</td>
      <td>10.408846</td>
      <td>7.371510</td>
      <td>7.344209</td>
      <td>5.323869</td>
    </tr>
  </tbody>
</table>
</div>

Cuối cùng, tôi sử dụng `seaborn` để lập đồ thị cho dữ liệu trên. 

``` python 
#Plotting the data 

sns.lineplot(data=df_plot)
plt.legend().remove()
ax = plt.gca() 
ax.set_xlabel('Month')
ax.set_ylabel('Percentage of Job Postings')
import matplotlib.ticker as mtick
ax.yaxis.set_major_formatter(mtick.FuncFormatter(lambda y, _: '{:.0%}'.format(y / 100)))
for i in range(5): 
    column_name = df_plot.columns[i]
    y_position = df_plot.iloc[-1, i]

    # Adjust the position only for 'python'
    if column_name == 'python':
        plt.text(x=11.2, y=y_position - 0.5,  # Move Python label up
                 s=column_name, color='black')
    else:
        plt.text(x=11.2, y=y_position, 
                 s=column_name, color='black')

ax.spines['top'].set_visible(False)
ax.spines['right'].set_visible(False)
plt.suptitle('Top 5 skills in Data Analyst job postings in the US')
plt.tight_layout()

``` 

### Kết quả 

![alt text](Images/2_Skills_Trend.png) 

### Thông tin rút ra 

* **SQL là kỹ năng được ưa chuộng nhất xuyên suốt năm** 

SQL luôn xuất hiện với tỷ lệ cao nhất trong các tin tuyển dụng Data Analyst, dao động khoảng 14% trước khi giảm nhẹ vào cuối năm. Điều này khẳng định SQL là một kỹ năng nền tảng đối với các nhà phân tích dữ liệu. 

* **Excel là kỹ năng được tìm kiếm nhiều thứ hai** 

Excel vẫn giữ được nhu cầu cao nhưng có xu hướng giảm dần theo thời gian, cho thấy khả năng chuyển dịch sang các công cụ nâng cao hơn để xử lý và trực quan hóa dữ liệu. 

* **Python và Tableau ngày càng quan trọng** 

Cả Python và Tableau đều có nhu cầu ổn định với một số biến động nhỏ. Điều này cho thấy các công ty ngày càng tìm kiếm những nhà phân tích có khả năng thực hiện phân tích dựa trên lập trình và trực quan hóa dữ liệu bên cạnh các công cụ truyền thống như Excel. 

## 3. Mức lương của sáu công việc phổ biến nhất tại Hoa Kỳ là bao nhiêu? 

### Phân tích sơ bộ 
Version chi tiết:  [3_Salary_Analysis.ipynb](3_Salary_Analysis.ipynb)  

Để xác định sáu công việc phổ biến nhất ở Hoa Kỳ, tôi đã đếm số lần xuất hiện của từng công việc trong DataFrame và chọn ra sáu công việc có số lượng cao nhất.

Sáu công việc phổ biến nhất là: Data Analyst, Data Scientist, Data Engineer, Senior Data Scientist, Senior Data Analyst và Senior Data Engineer.

Tiếp theo, tôi lọc tập dữ liệu để chỉ bao gồm các tin tuyển dụng cho sáu vai trò này.

Cuối cùng, tôi sử dụng `seaborn` để tạo một biểu đồ boxplot. 

``` python 
import seaborn as sns 
import matplotlib.ticker as mtick

#Plot the boxplot in order of highest to lowest median salary 
order = df_US.groupby('job_title_short')['salary_year_avg'].median().sort_values(ascending=False).index.tolist() 

sns.boxplot(df_US,x='salary_year_avg',y='job_title_short',order=order) 
plt.xlim(0,600000)
plt.xlabel("Average Salary (USD)")
plt.ylabel("")
plt.title("Average Salary by Job Title")
ax = plt.gca()
ax.xaxis.set_major_formatter(mtick.FuncFormatter(lambda x, _: f'{int(x/1000)}K'))

```

### Kết quả 
![alt text](Images/3_Salary_Analysis.png)  

### Thông tin rút ra 

* **Các vị trí cấp cao có mức lương cao hơn đáng kể** 

Senior Data Scientist và Senior Data Engineer có mức lương trung bình cao nhất, vượt xa các nghề còn lại. Điều này cho thấy kinh nghiệm dẫn đến mức lương cao hơn đáng kể trong các ngành nghề liên quan đến dữ liệu. 

* **Data Analyst có mức lương thấp nhất** 

Trong sáu vai trò, Data Analyst có mức lương trung bình thấp nhất và phạm vi lương tổng thể hẹp nhất. Điều này cho thấy rằng mặc dù đây là một điểm khởi đầu phổ biến trong sự nghiệp dữ liệu, nhưng tiềm năng thu nhập thấp hơn so với các vai trò trong lĩnh vực data. 

## 4. Những kỹ năng tối ưu nhất cho Data Analyst là gì? 

### Phân tích sơ bộ 
Version chi tiết: [4_Optimal_Skills.ipynb](4_Optimal_Skills.ipynb) 

Để tìm các kỹ năng tối ưu nhất cho Data Analyst, trước tiên tôi đã sử dụng hàm `.groupby()` để tạo một DataFrame, trong đó đếm số lần xuất hiện của mỗi kỹ năng trong tất cả các job posting và tính toán mức lương trung bình tương ứng. 

```python 
df_data = df_US.groupby('job_skills')['salary_year_avg'].agg(
    skill_count = 'count',
    median_salary = 'median')
``` 
Để làm rõ dữ liệu hơn, tôi sẽ sử dụng tỷ lệ phần trăm để cung cấp cái nhìn rõ ràng hơn về tần suất xuất hiện của mỗi kỹ năng. Cụ thể, tôi sẽ chia cột `skill_count` cho số lượng công việc 'Data Analyst' trong DataFrame gốc. 

```python 
df_data['skill_percent'] = df_data['skill_count'] / len(df[df['job_title_short'] == 'Data Analyst']) * 100 
``` 

Kết quả như sau: 

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>skill_count</th>
      <th>median_salary</th>
      <th>skill_percent</th>
    </tr>
    <tr>
      <th>job_skills</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>sql</th>
      <td>3079</td>
      <td>92500.0</td>
      <td>56.485049</td>
    </tr>
    <tr>
      <th>excel</th>
      <td>2135</td>
      <td>84479.0</td>
      <td>39.167125</td>
    </tr>
    <tr>
      <th>python</th>
      <td>1838</td>
      <td>98500.0</td>
      <td>33.718584</td>
    </tr>
    <tr>
      <th>tableau</th>
      <td>1657</td>
      <td>95000.0</td>
      <td>30.398092</td>
    </tr>
    <tr>
      <th>r</th>
      <td>1073</td>
      <td>92527.5</td>
      <td>19.684462</td>
    </tr>
    <tr>
      <th>power bi</th>
      <td>1042</td>
      <td>90000.0</td>
      <td>19.115759</td>
    </tr>
    <tr>
      <th>sas</th>
      <td>1006</td>
      <td>90000.0</td>
      <td>18.455329</td>
    </tr>
    <tr>
      <th>word</th>
      <td>523</td>
      <td>80000.0</td>
      <td>9.594570</td>
    </tr>
    <tr>
      <th>powerpoint</th>
      <td>518</td>
      <td>85000.0</td>
      <td>9.502844</td>
    </tr>
    <tr>
      <th>sql server</th>
      <td>336</td>
      <td>92150.0</td>
      <td>6.164007</td>
    </tr>
    <tr>
      <th>oracle</th>
      <td>332</td>
      <td>95000.0</td>
      <td>6.090626</td>
    </tr>
    <tr>
      <th>azure</th>
      <td>312</td>
      <td>100000.0</td>
      <td>5.723720</td>
    </tr>
    <tr>
      <th>aws</th>
      <td>294</td>
      <td>100500.0</td>
      <td>5.393506</td>
    </tr>
    <tr>
      <th>go</th>
      <td>288</td>
      <td>90000.0</td>
      <td>5.283434</td>
    </tr>
  </tbody>
</table>
</div>

Cuối cùng, tôi sử dụng `seaborn` để tạo ra một biểu đồ phân tán (scatter plot). 

```python 
sns.scatterplot(data=df_data,x='skill_percent',y='median_salary')
plt.xlim(0,65)

ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K'))
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos: f'{int(x)}%'))
plt.xlabel('Percentage of job postings that mention skill')
plt.ylabel('Median salary') 
plt.title('Median salary vs. skill frequency in job postings') 

texts = []
for i, txt in enumerate(df_data.index):
    texts.append(plt.text(df_data['skill_percent'].iloc[i], df_data['median_salary'].iloc[i]," " + txt))
from adjustText import adjust_text
adjust_text(texts, arrowprops=dict(arrowstyle='->', color='gray')) 

plt.tight_layout()
plt.show()
``` 

### Kết quả 
![alt text](Images/4_Optimal_Skills.png) 

### Thông tin rút được 

* **Kỹ năng liên quan tới Cloud (AWS & Azure) dẫn đến mức lương cao hơn** 

AWS và Azure có mức lương trung bình cao nhất, khoảng 100.000 USD, mặc dù chỉ xuất hiện số ít lần trong thông tin tuyển dụng. Điều này cho thấy các kỹ năng này có giá trị cao nhưng vẫn còn khan hiếm, dẫn đến mức lương hấp dẫn hơn. 

* **Python là kỹ năng thu hút nhà tuyển dụng và có tiềm năng trả lương cao** 

Python là một kỹ năng rất giá trị, xuất hiện trong khoảng 30% tin tuyển dụng với mức lương trung bình gần 98.000 USD. Python mang lại mức lương cao hơn so với SQL, cho thấy đây là một kỹ năng chuyên sâu và có tính khác biệt cao. Python được sử dụng rộng rãi trong khoa học dữ liệu. Đồng thời, Python có tính ứng dụng đa ngành, giúp mở rộng cơ hội nghề nghiệp. 

* **Kỹ năng văn phòng cơ bản (Excel, PowerPoint, Word) có mức lương thấp nhất** 

Các kỹ năng như Excel, PowerPoint và Word xuất hiện trong nhiều tin tuyển dụng nhưng có mức lương trung bình thấp nhất (khoảng 80.000–85.000 USD). Những công cụ này được sử dụng phổ biến và được kỳ vọng trong hầu hết các vai trò kinh doanh, do đó không tạo ra sự khác biệt lớn về tiềm năng thu nhập.
