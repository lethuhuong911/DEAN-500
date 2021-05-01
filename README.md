# DEAN-500


import numpy as np
import pandas as pd
from sklearn import tree

input_file = "/users/huongle/Desktop/breast-cancer-wisconsin.csv"
df = pd.read_csv(input_file, header = None)

df_new = df.rename(columns={0: "Sample_code_number", 1: "Clump_Thickness",  
                                    2: "Uniformity_of_Cell_Size", 3: "Uniformity_of_Cell_Shape",
                                    4: "Marginal_Adhesion", 5: "Single_Epithelial_Cell_Size",
                                    6: "Bare_Nuclei", 7: "Bland_Chromatin", 8: "Normal_Nucleoli",
                                   9: "Mitoses", 10: "Class"})
                            
#checking the missing values 

df_new = df_new.replace('?',np.NaN)

print('Number of instances = %d' % (df_new.shape[0]))
print('Number of attributes = %d' % (df_new.shape[1]))

print('Number of missing values:')
for col in df_new.columns:
    print('\t%s: %d' % (col,df_new[col].isna().sum()))



#The result shows that only 'Bare Nuclei' has 16 missing values 
#so I drop the missing values as shown below

print('Number of rows in original data = %d' % (df_new.shape[0]))

df_new1 = df_new.dropna()
print('Number of rows after removing missing values = %d' % (df_new1.shape[0]))


#remove outlier
%matplotlib inline

df_new2 = df_new1.drop(['Sample_code_number'], axis=1)
df_new2['Bare_Nuclei'] = pd.to_numeric(df_new2['Bare_Nuclei'])
df_new2.boxplot(figsize=(20,3))
