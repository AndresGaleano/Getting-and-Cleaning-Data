The data base contains the following variables:

-Subject number (or ID), ranging from 1 to 30.
-Activity name (activity ID not included) corresponding to the activity performed: 6 in total.
-3 spatial axis (x,y and z) and 2 devices (accelerometer for acceleration and gyroscope for velocity/speed). Acceleration is split in body and gravity acceleration. Two transformations, to obtain magnitude and frequency domain signals. For each, we obtain the mean and the standard deviation of each observation and then average them by subject and activity (6*30=180 rows).
In total, we have 2 identifiers (activity and subject number) and 33(33 different measurementes)*2(mean and std) variables.
