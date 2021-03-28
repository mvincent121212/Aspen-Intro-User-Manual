---
title: Calculator
keywords: sensitivity, calculator, design spec, model analysis, guess
last_updated: March 26, 2021
permalink: mydoc1_calculator.html
sidebar: mydoc1_sidebar
summary: You can use Aspen's calculator to find values for your simulation that Aspen does not automatically calculate.
---

This section uses the example setup given in the [Model Analysis Tools Intro](mydoc1_model_analysis_tools){:target="_blank"}.

Suppose we want to use our simulation results to find the relative volatility of our column. Aspen does not automatically calculate the relative volatility, but we can luckily calculate it ourselves using the Calculator block.

Navigate to **Flowsheeting Options** &#8594; **Calculator** in the Simulation browser to the left. Click "New" and in the pop-up window enter ID "RV" (for relative volatility).

The resulting window that pops up is the new "RV" Calculator instance that we have created.

## Define

The first tab that appears is **Define**. In this tab, we need to define every variable that we need to calculate the relative volatility. The equation for relative volatility for two components is:

<p align="center">
    <img src="images/calculator_rv.png">
</p>

In this case, `yi` and `xi` are the concentrations of ethanol in the vapor phase and liquid phase, respectfully. Similarly, `yj` and `xj` are the concentrations of water in the vapor and liquid phases. `yi/xi` can be rewritten as `Ki` and `yj/xj` can be rewritten as `Kj`. If you need more information on what relative volatility is, [refer to this website](https://www.separationprocesses.com/Distillation/DT_Chp01-3.htm){:target="_blank"}. However, what is more important is noticing that to calculate our relative volatility, we need to ask for variables `yi, xi, yj, and xj` from Aspen! Let's do this in the define tab.

Click "New" and when asked for a variable name enter "YE". This will be our y value of ethanol, or `yi`. Now we need to find where Aspen stores `yi` in its results. In "Category", select Streams, and in "Reference", select Mole-Frac, your overhead stream, and ethanol from all of the drop-down menus. In "Information Flow", select Import Variable. By specifying it is an Import Variable, you are saying that you are inputting this variable to calculate something else.

Your define tab should look like this:

<p align="center">
    <img src="images/calculator_ye.png">
</p>

Now we need to define three other variables named XE, YW, and XW. Repeat the same process for three more variables, asking for:
*  XE as the mole fraction of ethanol in the bottoms stream
*  YW as the mole fraction of water in the overhead stream
*  XW as the mole fraction of water in the bottoms stream

When you are done, scroll through your variables and make sure you have all four. We now need to define one variable that will save our value that we calculate for the relative volatility. Click "New" once more and enter "RV" for the variable name. Under "Category", select Model Utility. Under "Reference", select Parameter for Type and enter 1 for Parameter no. (every parameter that we specify must have its specific parameter number; since this is the first parameter we define, we give it the number 1). Finally in "Information Flow" select Export variable.

<p align="center">
    <img src="images/calculator_rv_var.png">
</p>

Our Define tab is complete! Next, click on the **Calculate** tab.

## Calculate

The **Calculate** tab asks that you enter the code that will calculate your equation. Under "Calculation Method", you can either enter a Fortran statement or import an excel spreadsheet. Although you likely have never used Fortran, it is generally easier to use this option than to import a spreadsheet unless you have an Excel sheet already prepared. For now, keep Fortran selected.

For your Fortran statement, enter your cursor on the far left of the window and hit the spacebar seven times (this was how I was taught how to do this, unfortunately). To check, make sure your cursor is on "Col: 7" which can be seen at the bottom of the window. Then enter the relative volatility equation:

<p align="center">
    <img src="images/calculator_fortran.png">
</p>

Your required input is now complete. Hit **Run** in the top left.

## Display Results

To find your results, click on **Flowsheeting Options** &#8594; **Calculator** &#8594; **RV** &#8594; **Results**. Then click on the **Define Variable** tab. Your results should display as a table where the "Value read" column shows what values Aspen read from your input variables and the "Value written" column shows what was calculated for your export variable(s).

<p align="center">
    <img src="images/calculator_results.png">
</p>

## Next Steps
*  [Sensitivity](mydoc1_sensitivity)
*  [Design Spec](mydoc1_designspec)

