---
title: Design Spec
keywords: sensitivity, calculator, design spec, model analysis, guess
last_updated: March 26, 2021
permalink: mydoc1_designspec.html
sidebar: mydoc1_sidebar
summary: You can use a design spec to find a specific value that you want out of your simulation. This value is found by changing one operating condition.
---

This section uses the example setup given in the [Model Analysis Tools Intro](/mydoc1_model_analysis_tools){:target="_blank"}.

We've found in the [Sensitivity section](/mydoc1_sensitivity){:target="blank"} that you can use Aspen to give you a table of how changing a variable will alter certain conditions of your simulation, like how changing the operating pressure will change the product's relative volatility. However, what if you want to find the specific operating conditions that give you a certain result from your simulation?

For example, let's say that your operator at your chemical plant assigns you to find what vapor fraction of the flash block is required to get 40 mol% of ethanol in the overhead stream. You could run a sensitivity analysis, but it might be difficult finding the exact value (you might need to put hundreds or thousands of points in your table to find your exact value). 

What is often easier for this type of problem is to use the Design Spec tool. Aspen's design spec will change the vapor fraction in your simulation until it finds exactly 40 mol% ethanol in your overhead product. Let's explore how to find the vapor fraction needed for your flash column in this section.

To navigate to the Design Spec, click on **Flowsheeting Options** &#8594; **Design Specs** in the Simulation browser. Click on "New" in the resulting menu, and accept the default name.

## Define
The **Define** tab asks what variable you want to find, or optimize, in your simulation. In this case, we want to find the purity of ethanol in the overhead stream.

Click "New" and then for variable name enter "EPURITY" (the name can be whatever you want). To define EPURITY as the purity of ethanol in the overhead, select Streams under "Category" and Mole-Frac, OVRHD (or the name of your overhead stream), and ETHANOL under "Reference".

<p align="center">
    <img src="images/designspec_define.png">
</p>

Your input for this tab should be complete. Next, click on **Spec** at the top.

## Spec
The **Spec** tab asks what your target value is for your variable that you defined in the last tab. In "Spec", enter "EPURITY" or whatever you named the variable in the Define tab.
{% include note.html content="The spec that you enter in the **Spec** tab must match the variable that you made in the **Define** tab." %}

The "target" value is what value you want your spec to be. Enter 0.4 for this value.

The "tolerance" value is how far away the simulation is allowed to be from the target value. For example, if you entered 0.1 for the tolerance, you are allowing the simulation to return a final value as far away as 0.39 or 0.41 instead of 0.4. It might be useful to input a large tolerance if it will be difficult for the simulation to obtain the target. However, for this example we can get the spec pretty close to the target. Enter 0.0001 for the tolerance.

<p align="center">
    <img src="images/designspec_spec.png">
</p>

The required input should be complete. Next, click on the **Vary** tab.

## Vary

The **Vary** tab tells Aspen what variable it should vary to find the target value in **Spec**. We want to vary the vapor fraction. In "Manipulated variable", find VFRAC under Block-Var and your flash block name. For the "Manipulated variable limits", enter a lower of 0.15 and an upper of 0.5.

<p align="center">
    <img src="images/designspec_vary.png">
</p>

All of the required input for the design spec should now be complete! Hit **Run**.

## Display Results

Find your results under **Flowsheeting Options** &#8594; **Design Specs** &#8594; **DS-1** &#8594; **Results**. The "Initial value" column tells you what the variables were before the design spec was used. The "Final value" is what the design spec converged to.

<p align="center">
    <img src="images/designspec_results.png">
</p>
{% include note.html content="Notice that the final value for your purity is within the bounds of your tolerance." %}






