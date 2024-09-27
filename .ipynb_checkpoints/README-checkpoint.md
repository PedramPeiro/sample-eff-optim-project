Read me 


There are two components to this folder, the 1intersection_straight_traffic_travel_time_analysis and the Bayesian Simulation+Ground Truth. 

————————————————————————————————————————————————

the 1intersection_straight_traffic_travel_time_analysis is an analysis based on one intersection SUMO simulations which derives a function that describes the relationship between green time and average travel time (across different freeflow travel times : edge length / speed limit). 

Through different fittings, a polynomial relationship is derived which will be used in the custom kernel build in the bayesian simulation. 

Final model is:
    travel_time = 2.40458665e+03  -1.22774788e+02 * green_time_in_seconds -8.77530322e-01 * free_flow_travel_time_in_seconds +
    2.12125825e+00 * (green_time_in_seconds**2) + 3.05518676e-02 * ( free_flow_travel_time_in_seconds**2) +
    -1.21699366e-02 * (green_time_in_seconds**3) -5.53583776e-05 * ( free_flow_travel_time_in_seconds**3)

The process of fitting you can find in notebook 4 (travel_time_green_time_analysis.ipynb)
Notebook 1, 2, 3 are the SUMO experiment data input and output that lead up to the data for notebook 4

————————————————————————————————————————————————

The purpose of the bayesian experiment is to see if the custom kernel can perform well in approximating the green times given ground truth travel times (from the ), exploring the polynomial relationship between green time and average travel times in addition to the Matern kernel. 

The Bayesian Simulation folder with the main notebook Matern_variations_bayesian.ipynb run the Gaussian process on the 3 intersections (thus 3 green times), with the emphasis on the Gaussian Process model with Custom kernel (a custom matern kernel multiplied by custom component of the polynomial). For more information on the custom kernel, please check the kernel exploration output.pptx

The key functions in the notebook is CustomKernelwMatern, which defines the custom kernel that uses fA(x) the polynomial, the rest is pretty standard Bayesian Optimization setup inherited from vanilla_bo notebook. 

The 3 intersections network looks like this: (the 1 intersection analysis is simply 1 intersection version of the network)

![Alt text](3intersections_demo.png)



