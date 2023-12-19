.. _orca:

Introduction
============

**O**\ ptimization for **R**\ eal-time **C**\ apacity **A**\ llocation (ORCA) is
 a software platform for creating and running real-time control and optimization
 workflows for Integrated Energy Systems (IES). The IES program aims to increase
 flexibility in nuclear energy generation to allow nuclear plants to thrive
 economically while supporting variable grid demand. A key mechanism for
 implementing such flexibility would be to use excess heat and electricity
 (available at times of low net electricity demand) for hydrogen production,
 water desalination, thermal storage, or other industrial processes. To enable
 responsive generation for various industrial processes, an IES needs a control
 system to support dynamically incorporating multiapplication energy systems and
 apportion thermal or electrical energy. The demonstration of such a control system
 is critical for tightly coupled and thermally coupled IESs, where optimizations
 and controls are needed for multiple components and connection points. ORCA is
 developed to maximize the revenue of NPPs by efficiently operating multiapplication
 energy systems. The ORCA workflow is based on a receding-horizon- or economic model
 predictive control(EMPC)-based optimization. EMPC uses a dynamic model to optimize
 an objective function over a finite time horizon. The essence of EMPC is to optimize,
 over the manipulatable inputs, forecasts of process behaviors subject to equality
 and inequality constraints. The forecasting is performed using a process model
 (i.e., a predictor) over a finite time interval of length .

ORCA can be used via individual components or with the `CollectedNextDispatch` object.

The `Optimization` and `RewardForecast` objects are intended to have a simple, cohesive
interface that allows plug and play use. Each `Optimization` object is required to have
a `return_next_dispatch` method that performs the optimization and returns the next time
step's optimal dispatch. Each `RewardForecast` object is required to have a `gen_reward`
method that returns n samples of the reward/price data required in the time horizon for
optimization. New optimization or reward forecast algorithms may be implemented and when
placed in the appropriate directory, the `CollectedNextDispatch` object can find and use
them or they may be used independently for optimization workflows.

The `CollectedNextDispatch` object instantiates the required `Optimization` and
`RewardForecast` objects specified in a YAML file. Note that only one `Optimization`
object is required, but many `RewardForecast` objects may be specified to represent
reward/price information of multiple components. An example of a YAML specification file
is given in `notebooks/CollectedNextDispatchExample.yaml`.