README — Hybrid MIMO Neural ODE + MPC Controller


Author: Pranav & Divyang  
Project: Hybrid Physics-Informed MIMO Neural ODE with MPC  
Course: ME 691 XVII (Scientific Machine Learning)


1. Project Overview


This project develops a Hybrid MIMO Neural ODE model to learn 
the thermal dynamics of a dual-heater system. The model combines:


• Physics module (cooling, heating gains, coupling)
• Residual neural network (SiLU activation)
• RK4 time integration
• Trained on 3 experiment sheets (Sheet 1,2 only – Sheet 3,4 skipped)
• Environment temperature included as input


The learned model is then used inside a Model Predictive Control (MPC)
framework to track a desired temperature setpoint using only heater commands.


2. File Description


1) Project_sciml_Pranav_Divyang.ipynb
   - Main notebook containing the entire workflow:
        • Data loading + preprocessing
        • Hybrid MIMO Neural ODE model definition
        • Physics module + residual NN
        • RK4 integrator
        • Training loop (per-sheet training)
        • Training loss plots
        • MIMO model validation plots
        • MPC formulation (cost function + constraints)
        • Full MPC closed-loop simulation
        • Final temperature, heater and cost plots


   - This is the ONLY required file to run the project.


3. How to Run the Notebook


Step 1 — Install dependencies  
Make sure the following Python packages are installed:


• numpy
• pandas
• matplotlib
• scipy
• torch
• openpyxl (for Excel sheet reading)


Install using:
    pip install numpy pandas matplotlib scipy torch openpyxl


Step 2 — Place your dataset
Download the dataset and replace the file path with yours.


Step 3 — Open the notebook
Run the notebook cell-by-cell in:


• Jupyter Notebook  
or  
• Google Colab (upload file + notebook)


Step 4 — Train the Hybrid Model
Run the training section:
    - HybridMIMO model is created.
    - Each sheet is trained sequentially.
    - Loss plot is displayed.


Step 5 — Validate Thermal Dynamics
Run the “MIMO Test” cell to verify model behaviour:
    • Heating curves  
    • Cross-coupling  
    • Stability  


Step 6 — Run MPC Simulation
Scroll to the MPC section and run:
    t_log, x_log_K, u_log_perc, cost_log = run_mpc(...)


Outputs:
    • Temperature vs time  
    • Heater percentage commands  
    • MPC cost  
    • Convergence to 40°C setpoint  (you can change the setpoint by changing the values of variable SETPOINT_C)


4. Notes
• Sheet 3 and 4 are intentionally ignored because one heater
  was always zero → leads to bad gradients.


• The MPC uses:
      – Real plant ODE (Kelvin) for state propagation  
      – Learned hybrid model for prediction  


• The controller achieves smooth convergence with minimal overshoot.


5. Reproducibility


To reproduce exactly:
  1. Use same dataset ("ML DATA-2.xlsx")
  2. Leave random seeds fixed in the notebook
  3. Use PyTorch CPU/GPU consistently
  4. Re-run all cells in order