# Group50
travel time estimation project of xun xu and yingzhe luo

This file includes the report named TRAVEL_TIME_ESTIMATION, the latex codes, and the codes.

Upload all things in the file latexcodes, you can get my report using overleaf.

--------------------------------------------------------------------

How to use the code?

Model Training
python train.py

Parameters:

* task: train/test
* batch_size: the batch_size to train, default 400
* epochs: the epoch to train, default 100
* kernel_size: the kernel size of Geo-Conv, only used when the model contains the Geo-conv part
* pooling_method: attention/mean
* alpha: the weight of combination in multi-task learning
* log_file: the path of log file
* result_file: the path to save the predict result. By default, this switch is off during the training

Example:

 python main.py --task train  --batch_size 10  --result_file ./result/deeptte.res --pooling_method attention --kernel_size 3 --alpha 0.1 --log_file run_log


Model Evaluation

Parameters:
* weight_file: the path of model weight
* result_file: the path to save the result

Example:

python main.py --task test --weight_file ./saved_weights/weight --batch_size 10  --result_file ./result/deeptte.res --pooling_method attention --kernel_size 3 --alpha 0.1


Format Instructions
Each sample is a json string. The key contains:
* driverID
* dateID: the date in a month, from 0 to 30
* weekID: the day of week, from 0 to 6 (Mon to Sun)
* timeID: the ID of the start time (in minute), from 0 to 1439
* dist: total distance of the path (KM)
* time: total travel time (min), i.e., the ground truth. You can set it as any value during the test phase
* lngs: the sequence of longitutes of all sampled GPS points
* lats: the sequence of latitudes of all sampled GPS points
* states: the sequence of taxi states (available/unavaible). You can remove this attributes if it is not available in your dataset. See models/base/Attr.py for details.
* time_gap: the same length as lngs. Each value indicates the time gap from current point to the firt point (set it as arbitrary values during the test)
* dist_gap: the same as time_gap
