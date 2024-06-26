# b10090115
MachineLearning
from sklearn import svm, datasets
from sklearn.model_selection import GridSearchCV
# 載入鳶尾花朵資料集
iris = datasets.load_iris()
# 設定想要的搜索參數並給予候選值
parameters = {'kernel':('linear', 'rbf'), 'C':[1, 10]}
# 建立 SVC 分類器
svc = svm.SVC()
# 網格搜索所有可能的組合(2*2)共四種
clf = GridSearchCV(svc, parameters)
# 擬合數據並回傳最佳模型
clf.fit(iris.data, iris.target)

from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import RandomizedSearchCV
from scipy.stats import uniform
# 載入鳶尾花朵資料集
# 建立邏輯迴歸模型
logistic = LogisticRegression(solver='saga', tol=1e-2, max_iter=200, random_state=0)
# 設定欲搜尋的超參數並給予一個期望的範圍
distributions = dict(C=uniform(loc=0, scale=4),
                     penalty=['l2', 'l1'])
# 隨機搜索預設 n_iter=10
clf = RandomizedSearchCV(logistic, distributions, random_state=0, n_iter=10)
# 擬合數據並回傳最佳模型
search = clf.fit(iris.data, iris.target)
search.best_params_
search.cv_results_
