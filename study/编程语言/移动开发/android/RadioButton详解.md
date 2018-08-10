RadioButton和CheckBox的区别：

* 单个RadioButton在选中后，通过点击无法变为未选中。单个CheckBox在选中后，通过点击可以变为未选中。

* 一组RadioButton，只能同时选中一个。 一组CheckBox，能同时选中多个 

* RadioButton在大部分UI框架中默认都以圆形表示。CheckBox在大部分UI框架中默认都以矩形表示 

RadioButton和RadioGroup的关系：

* RadioButton表示单个圆形单选框，而RadioGroup是可以容纳多个RadioButton的容器 
 
* 每个RadioGroup中的RadioButton同时只能有一个被选中 
 
* 不同的RadioGroup中的RadioButton互不相干，即如果组A中有一个选中了，组B中依然可以有一个被选中 
 
* 大部分场合下，一个RadioGroup中至少有2个RadioButton 

* 大部分场合下，一个RadioGroup中的RadioButton默认会有一个被选中，并建议您将它放在RadioGroup中的起始位置