Handout files:

readme.txt - this file
ais_train.csv - training data       
ais_test.csv - test input data 
schedules_to_may_2024.csv - optional data that contains schedules for some vessels  
ports.csv - optional data related to ports           
vessels.csv - optional data related to vessels         
ais_sample_submission.csv - a demo submission to Kaggle what predicts all zeroes 
Dataset definitions and explanation.docx - a documents that gives more details about the dataset and column names  
Machine learning task for TDT4173.docx - brief introduction to the task
vessel_trajectories_visualization.ipynb - a demo utility function for visualizing the trajectory of a vessel
kaggle_metric.ipynb - the score function we use in the Kaggle competition

Submission files:

Report.ipynb - Main report 
Short_notebook_1.ipynb - Short notebook to reproduce kaggel submission
Short_notebook_2.ipynb - Short notebook to reproduce a different kaggel submission

Problem Description and context:

Given AIS data from January 1st to May 7th, 2024, predict the future positions of vessels at specific timestamps for five days into the future. Students were tasked with developing predictive models that account for various factors such as congestion, port calls, and other events affecting the vessels' journeys.

The challenge with the dataset was that the AIS data we received was limited to signals from vessels reporting approximately every 20 minutes to land stations with a range of about 30 km. This resulted in vessels "disappearing" from the dataset for anywhere from a few hours to up to 30 days when they moved away from land. Consequently, all typical time-series frameworks were rendered ineffective, and common benchmark solutions like LSTM neural networks were only suitable for short-horizon predictions.

The solution therefore relied on very simple tree-based models. My model was based on using the last observed information to generate all future predictions, effectively employing a multi-step prediction framework. I also attempted iterative prediction, but the model struggled to learn time patterns or to handle jumps/teleportation in the data.

The test data was prepared by forward-filling the last observed position and speed as covariates for 5-day intervals. The idea was to train the model on data as similar as possible to the test data. Temporal dependency was modeled as the time elapsed since the last observed position. Surprisingly, this simple model achieved impressive R² scores and handled vessel teleportation far better than more complex models. Adding more features typically introduced more noise, with variables showing high split importance but no gain importance.
