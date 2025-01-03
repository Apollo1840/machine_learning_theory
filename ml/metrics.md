
### classification evaluation

| TP | FP | TN | FN |
| ---- | ---- | ---- | ---- | 

accuracy: T/A

sensitivity: TP/P

specificity: TN/N

ROC: sensitivity(x) to 1-specificity(y)

Imagine, you have several apples, some are good, some are bad. You ask your child (the model) to pick them: keep the good apples, and throw the bad apples. 

True is the good apples kept and the bad apples thrown.

False is the bad apples kept (Error I) and the good apples thrown (Error II).

Positive is the apples your child keep.

Negative is the apples your child thrown.

Accuracy is the True/All

There are two aspect to evaluate the model: precision and recall.

Precision is easy.

postive precision is the ratio of good apples compare to what your chlid kept.

negative precision is the ratio of of bad apples compare to what your child thrown.

Recall is more interesting.

positve recall (sensitivity) is the ratio of good apples you have compare to all good apples. 

negative recall (specifictiy) is the of ratio of bad apples your child thrown compare to all bad apples. 

