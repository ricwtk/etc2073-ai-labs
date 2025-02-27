# Lab 2: Fuzzy Systems

## Lab learning outcomes
After completing this lab, the students are able to

- construct a Mamdani fuzzy system using the `scikit-fuzzy` Python library and
- evaluate the result of the constructed fuzzy system.

## Note
Install the `scikit-fuzzy` Python library in your environment before proceeding with the lab.

```python
conda install -c conda-forge scikit-fuzzy
```

## Fuzzy control system for a train

1. Consider a fuzzy control system to control the **brake** and **throttle** of a train based on the **speed** of the train and the **distance** of the train to the next stop.

2. Import the `skfuzzy`, `skfuzzy.control`, and `numpy`.

    ```python
    import numpy as np
    from skfuzzy import control as ctrl
    from skfuzzy import membership as mf
    ```

### Initialise inputs and outputs

1. Speed and distance are the inputs of the system whereas brake and throttle are the outputs.

2. The ranges for the variables are:

    |Variable|Range|
    |:--------|:-----:|
    |Speed   | 0 - 85 km/h |
    |Distance| 0 - 3000 m  |
    |Brake   | 0 - 100%    |
    |Throttle| 0 - 100%    |


3. As the inputs will be the antecedents of the rules, construct the variables `speed` and `distance` as `skfuzzy.control.Antecedent` objects. 

    ```python
    speed = ctrl.Antecedent(np.arange(0, 85, 0.1), 'speed')
    ```

4. The initialisation function for `skfuzzy.control.Antecedent` object takes 2 arguments, the first is the *universe* of the variable, i.e. the values the variables can take, the second is the label of the variable. The initialisation function for `skfuzzy.control.Consequent` is similar. 

5. The label and the range of the variable can be accessed using `.label` and `.universe` respectively.

<div style='margin-top: 20px'></div>

**Task**: Initialise the variables `distance` as `Antecedent` object, and `brake` and `throttle` as `Consequent` objects. (Outputs of the system will be consequents of the rules)

### Define membership functions for fuzzy sets of variables

1. The fit vectors of the fuzzy sets for the linguistic variables are given as follows:

    - speed (0 to 85 km/h)

        |Linguistic value|Fit vector           |
        |----------------|---------------------|
        |Stopped         |(1/0, 0/2)            |
        |Very slow       |(0/1, 1/2.5, 0/4)      |
        |Slow            |(0/2.5, 1/6.5, 0/10.5) |
        |Medium fast     |(0/6.5, 1/26.5, 0/46.5)|
        |Fast            |(0/26.5, 1/70, 1/85)   |

    - distance (0 to 3000 m)

        |Linguistic value|Fit vector            |
        |----------------|----------------------|
        |At              |(1/0, 0/2)             |
        |Very near       |(0/1, 1/3, 0/5)         |
        |Near            |(0/3, 1/101.5, 0/200)   |
        |Medium far      |(0/100, 1/1550, 0/3000) |
        |Far             |(0/1500, 1/2250, 1/3000)|


    - brake (0 to 100%)

        |Linguistic value|Fit vector|
        |----------------|----------|
        |No              |(1/0, 0/40)|
        |Very slight     |(0/20, 1/50, 0/80)|
        |Slight          |(0/70, 1/83.5, 0/97)|
        |Medium          |(0/95, 1/97, 0/99)|
        |Full            |(0/98, 1/100)|

    - throttle (0 to 100%)

        |Linguistic value|Fit vector|
        |----------------|----------|
        |No              |(1/0, 0/2)|
        |Very slight     |(0/1, 1/3, 0/5)|
        |Slight          |(0/3, 1/16.5, 0/30)|
        |Medium          |(0/20, 1/50, 0/80)|
        |Full            |(0/60, 1/80, 1/100)|

2. The `skfuzzy.membership` module provides the following membership functions:

    |Membership function |Description |
    |--------------------|------------|
    |`skfuzzy.membership.dsigmf(x, b1, c1, b2, c2)`|Difference of two fuzzy sigmoid membership functions|
    |`skfuzzy.membership.gauss2mf(x, mean1, ...)`|Gaussian fuzzy membership function of two combined Gaussians|
    |`skfuzzy.membership.gaussmf(x, mean, sigma)`|Gaussian fuzzy membership function|
    |`skfuzzy.membership.gbellmf(x, a, b, c)`|Generalized Bell function fuzzy membership generator|
    |`skfuzzy.membership.piecemf(x, abc)`|Piecewise linear membership function (particularly used in FIRE filters)|
    |`skfuzzy.membership.pimf(x, a, b, c, d)`|Pi-function fuzzy membership generator|
    |`skfuzzy.membership.psigmf(x, b1, c1, b2, c2)`|Product of two sigmoid membership functions|
    |`skfuzzy.membership.sigmf(x, b, c)`|The basic sigmoid membership function generator|
    |`skfuzzy.membership.smf(x, a, b)`|S-function fuzzy membership generator|
    |`skfuzzy.membership.trapmf(x, abcd)`|Trapezoidal membership function generator|
    |`skfuzzy.membership.trimf(x, abc)`|Triangular membership function generator|
    |`skfuzzy.membership.zmf(x, a, b)`|Z-function fuzzy membership generator|

3. The fit vector of a linguitic value can be assigned to a linguistic variable using

    ```python
    speed['stopped'] = mf.trimf(speed.universe, [0, 0, 2])
    speed['very slow'] = mf.trimf(speed.universe, [1, 2.5, 4])
    ```

    **Task**: Assign all fuzzy sets to the linguistic variables.

4. The fuzzy set diagram of a linguistic variable can be viewed using `.view()`

    ```python
    speed.view()
    ```

    **Task**: Check if the fuzzy set diagrams match the fit vectors.

### Define rules

1. The rules for this system are displayed in the following fuzzy association memory (FAM) representaion table.

    <div class="md-typeset__scrollwrap">
    <table class="fam-table">
    <tr>
      <td colspan='2'></td>
      <td colspan='5'>Distance</td>
    </tr>
    <tr>
      <td colspan='2'></td>
      <td>At</td>
      <td>Very near</td>
      <td>Near</td>
      <td>Medium far</td>
      <td>Far</td>
    </tr>
    <tr>
      <td rowspan='5'>Speed</td>
      <td>Stopped</td>
      <td>Full brake<br>No throttle</td>
      <td>Full brake<br>Very slight throttle</td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>Very slow</td>
      <td>Full brake<br>No throttle</td>
      <td>Medium brake<br>Very slight throttle</td>
      <td>Slight brake<br>Very slight throttle</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>Slow</td>
      <td>Full brake<br>No throttle</td>
      <td>Medium brake<br>Very slight throttle</td>
      <td>Very slight brake<br>Slight throttle</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>Medium fast</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Very slight brake<br>Medium throttle</td>
      <td>No brake<br>Full throttle</td>
    </tr>
    <tr>
      <td>Fast</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Very slight brake<br>Medium throttle</td>
      <td>No brake<br>Full throttle</td>
    </tr>
    </table>
    </div>

2. Rule can be defined using `skfuzzy.control.Rule(antecedent, consequent, label)`. To define the first rule, i.e. if distance is 'at' and speed is 'stopped', then full brake and no throttle, 

    ```python
    rule1 = ctrl.Rule(distance['at'] & speed['stopped'], (brake['full'], throttle['no']))
    ```

    If the antecedent consists of multiple parts, they can be combined using operators `|` (OR), `&` (AND), and `~` (NOT).

    If the consequent consists of multiple parts, they can be combined as a `list`/`tuple`.

    **Task**: Define all the rules. Then combine all the rules in a `list`, i.e. `rules = [rule1, rule2, ...]`.

### Construct the fuzzy control system
1. The train control system can be constructed with
    
    ```python
    train_ctrl = ctrl.ControlSystem(rules=rules)
    ```

2. A `skfuzzy.control.ControlSystemSimulation` object is needed to simulate the control system to obtain the outputs given certain inputs.

    ```python
    train = ctrl.ControlSystemSimulation(control_system=train_ctrl)
    ```

3. To obtain the values for `brake` and `throttle` given that `speed` is 30 km/h and `distance` is 6 m,

    ```python
    # define the values for the inputs
    train.input['speed'] = 30
    train.input['distance'] = 2000

    # compute the outputs
    train.compute()

    # print the output values
    print(train.output)

    # to extract one of the outputs
    print(train.output['brake'])
    ```

4. To view the results in the graph,

    ```python
    brake.view(sim=train)
    throttle.view(sim=train)
    ```

### View the control/output space

1. The control/output space allows us to identify if the outputs fit our expectation.

2. Construct an empty 3D space with 100-by-100 x-y grid.

    ```python
    x, y = np.meshgrid(np.linspace(speed.universe.min(), speed.universe.max(), 100),
                       np.linspace(distance.universe.min(), distance.universe.max(), 100))
    z_brake = np.zeros_like(x, dtype=float)
    z_throttle = np.zeros_like(x, dtype=float)
    ```

3. Loop through every point and identify the value of brake and throttle of each point. As the specified rules are not exhaustive, i.e. some input combinations do not activate any rule, we will set the output of such input combinations to be `float('inf')`.
    ```python
    for i,r in enumerate(x):
      for j,c in enumerate(r):
        train.input['speed'] = x[i,j]
        train.input['distance'] = y[i,j]
        train.compute()
        try:
          z_brake[i,j] = train.output['brake']
          z_throttle[i,j] = train.output['throttle']  
        except:
          z_brake[i,j] = float('inf')
          z_throttle[i,j] = float('inf')
    ```

4. Plot the result in a 3D graph using the `matplotlib.pyplot` library.

    ```python
    import matplotlib.pyplot as plt
    from mpl_toolkits.mplot3d import Axes3D

    def plot3d(x,y,z):
      fig = plt.figure()
      ax = fig.add_subplot(111, projection='3d')

      ax.plot_surface(x, y, z, rstride=1, cstride=1, cmap='viridis', linewidth=0.4, antialiased=True)

      ax.contourf(x, y, z, zdir='z', offset=-2.5, cmap='viridis', alpha=0.5)
      ax.contourf(x, y, z, zdir='x', offset=x.max()*1.5, cmap='viridis', alpha=0.5)
      ax.contourf(x, y, z, zdir='y', offset=y.max()*1.5, cmap='viridis', alpha=0.5)

      ax.view_init(30, 200)

    plot3d(x, y, z_brake)
    plot3d(x, y, z_throttle)
    ```

## Fuzzy tipping recommendation system

1. A fuzzy expert system is designed to identify the percentage of tips a customer will give based on the service and the food the customer received.

2. The system has service rating and food rating as inputs, and tips as output.

3. The fit vectors of the fuzzy sets for the linguistic variables are given as follows:

    - service (0 to 10)

        |Linguistic value|Fit vector           |
        |----------------|---------------------|
        |Poor            |(1/0, 0/5)           |
        |Average         |(0/0, 1/5, 0/10)     |
        |Good            |(0/5, 1/10)          |

    - food (0 to 10)

        |Linguistic value|Fit vector           |
        |----------------|---------------------|
        |Poor            |(1/0, 0/5)           |
        |Average         |(0/0, 1/5, 0/10)     |
        |Good            |(0/5, 1/10)          |
        
    - tips (0 to 30%)

        |Linguistic value|Fit vector           |
        |----------------|---------------------|
        |Low             |(1/0, 0/15)          |
        |Medium          |(0/0, 1/15, 0/30)    |
        |High            |(0/15, 1/30)         |

4. The rules are displayed in the following fuzzy association memory (FAM) representaion table.

    <div class="md-typeset__scrollwrap">
    <table class="fam-table">
    <tr>
      <td colspan='2'></td>
      <td colspan='3'>Food</td>
    </tr>
    <tr>
      <td colspan='2'></td>
      <td>Poor</td>
      <td>Average</td>
      <td>Good</td>
    </tr>
    <tr>
      <td rowspan='3'>Service</td>
      <td>Poor</td>
      <td>low tips</td>
      <td>low tips</td>
      <td>medium tips</td>
    </tr>
    <tr>
      <td>Average</td>
      <td>low tips</td>
      <td>medium tips</td>
      <td>high tips</td>
    </tr>
    <tr>
      <td>Good</td>
      <td>medium tips</td>
      <td>high tips</td>
      <td>high tips</td>
    </tr>
    </table>
    </div>

<div style='margin-top: 20px'></div>

**Task**: Construct the fuzzy inference system.

<div style='margin-top: 20px'></div>

**Task**: Discuss, if you were to make at least one modification to the fuzzy tipping recommendation system, what it will be and why.

## Report

Submit a report detailing the process, results, graphs, and your observations.