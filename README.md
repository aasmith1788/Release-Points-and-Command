# Release-Points-and-Command
Investigated the effect of release angles on pitch location using 2023 pitch-by-pitch Statcast data.
After reading this article, I learned release angles play a  part in determining location. While the author's main goal in his study was to find a better way to evaluate a pitcher’s command, I wanted to take a different direction by further exploring release angles and their relationship with biomechanics and location.. To begin, I created several random forest regressions models to help provide insight into  how release angles affect pitch location for lefties and righties. 2023 pitch by pitch statcast data was used for this analysis. 
Random Forest Regression
Horizontal Location  R-squared and Mean Squared Error
A random forest regression model was made to predict horizontal location for both lefties and righties. Below are the results. 

Left Handed Pitchers
Training Mean Squared Error: 0.010114236169265128

Training R^2 Score: 0.9850814910365222

Testing Mean Squared Error: 0.011976440453063036

Testing R^2 Score: 0.9822324868923841

Cross-Validation R^2 Scores: [0.98139265 0.98145445 0.98343365 0.98117009 0.97716173]

Average Cross-Validation R^2 Score: 0.9809225123251574

Right Handed Pitchers

Training Mean Squared Error: 0.01336922879412911

Training R^2 Score: 0.9808052307407897

Testing Mean Squared Error: 0.014537842286340995

Testing R^2 Score: 0.9791530285643611

Cross-Validation R^2 Scores: [0.98061139 0.98092879 0.97894936 0.97772955 0.97934016]

Average Cross-Validation R^2 Score: 0.9795118509052404


Horizontal Location Feature Importance

HRA (Horizontal Release Angle):  

LHP: Explained 38.5% of the variance

RHP: Explained 40.1% of the variance

For both lefties and righties the partial dependence plot for HRA shows a generally increasing trend. This indicates that as the horizontal release angle increases, the predicted horizontal location of the pitch moves further to the right side of the strike zone from the pitcher's perspective. Conversely, as the horizontal release angle decreases, the predicted horizontal location shifts to the left side of the zone from the pitcher's perspective.

pfx_x (Horizontal Movement): 

LHP: Explained 34.9% of the variance

RHP: Explained 33.1% of the variance

For both lefties and righties the partial dependence plot for pfx_x shows an increasing trend. This means that as the horizontal movement of the pitch increases (moving to the right), the predicted horizontal location of the pitch also moves to the right side of the strike zone from the pitcher's perspective. A decrease in pfx_x would predict the pitch moving to the left side of the zone.

release_pos_x (Release Side): 

LHP: Explained 25%  of the variance

RHP: Explained 28.4% of the variance

For both righties and lefties the partial dependence plot for release_pos_x shows an increasing trend. As the release position moves to the right side of the zone from the pitcher's perspective (more positive values), the predicted horizontal location also shifts to the right. If the release_pos_x decreases, the model predicts the pitch to be more to the left side of the zone.

Vertical Location  R-squared and Mean Squared Error

A random forest regression model was made to predict vertical location for both lefties and righties. Below are the results. 

Left Handed Pitchers

Training Mean Squared Error: 0.07416589926891601

Training R^2 Score: 0.9200212671941931

Testing Mean Squared Error: 0.0822561660842893

Testing R^2 Score: 0.9131506638890982

Cross-Validation R^2 Scores: [0.9014758  0.9138822  0.91088942 0.91490804 0.90933986]

Average Cross-Validation R^2 Score: 0.9100990630292725

Right Handed Pitchers

Training Mean Squared Error: 0.07658885291292229

Training R^2 Score: 0.9186156007482175

Testing Mean Squared Error: 0.08035933007697364

Testing R^2 Score: 0.9150120240411039

Cross-Validation R^2 Scores: [0.91569124 0.91025302 0.91439535 0.91466894 0.90752568]

Average Cross-Validation R^2 Score: 0.9125068445533341

Horizontal Location Feature Importance

VRA (Vertical Release Angle): 

LHP: Explained 42.3% of the variance

RHP: Explained 53.7% of the variance

For both lefties and righties the partial dependence plot for VRA shows an increasing trend. This indicates that as the vertical release angle increases, the predicted vertical location of the pitch moves higher in the strike  zone. Conversely, as the vertical release angle decreases, the predicted vertical location shifts lower in the zone.
pfx_z (Vertical Movement): 

LHP: Explained 45% of the variance

RHP: Explained 32.6% of the variance

For both righties and lefties the partial dependence plot for pfx_z shows an increasing trend with some variations. This means that as the vertical movement of the pitch increases, the predicted vertical location of the pitch also moves higher in the zone. A decrease in pfx_z would predict the pitch moving lower in the zone.


release_pos_z (Release Position Z): 

LHP: Explained 12.7% of the variance

RHP: Explained 13.6% of the variance

The partial dependence plot for release_pos_z shows an increasing trend. As the release position height increases, the predicted vertical location of the pitch also shifts higher in the zone. If the release_pos_z decreases, the model predicts the pitch to be lower in the zone.
How does this help us understand pitch location?

In all four models, release angle and movement (represented by pfx_) account for the majority of the variance. While pitch movement tends to remain fairly consistent within a game, release angles can vary. Theoretically, if pitchers can learn to manipulate these angles effectively, they should be able to exert better control over where the ball lands. This suggests that focusing on release angles could be a key strategy for improving pitch control.. However, simply telling a pitcher to decrease his vertical release angle to throw lower in the zone is often not practical and can result in the phenomenon known as “domed up.” This leads into the next portion of the project; which biomechanics are responsible for the variation in pitch release angles?  Unfortunately, this is where the project stalled. At best, I found only loose correlations related to horizontal and vertical release angles. 
For both right-handed and left-handed pitchers, spin axis had the largest correlation with horizontal release angles at 0.45 with an R-squared value of 0.20. The spin axis is defined as the ball's tilt in degrees from a vertical or horizontal line. For example, a perfectly back spinning fastball features a vertical spin axis, which typically results in the ball "rising" or dropping less than a batter would expect due solely to gravity. Conversely, a perfectly side spinning pitch, such as a slider, maintains a horizontal spin axis, leading it to move laterally. In terms of manipulating horizontal release angles, pitchers could potentially adjust their finger pressure and grip on the ball to directly influence the spin axis and release angles. These adjustments could potentially allow pitchers to more accurately locate their pitches horizontally, enhancing their ability to hit specific spots in the strike zone. 

For both right-handed and left-handed pitchers, trunk and pelvis angles at specific moments during their delivery showed the highest correlation with vertical release angles, with correlation coefficients at -0.4 and above, and R-squared values exceeding 0.2. As the trunk angle increases, the vertical release angle tends to decrease. Trunk angle is an indicator of arm slot, suggesting that the arm slot significantly influences vertical release angle. This observation aligns logically with pitching mechanics: pitchers with higher arm slots can generate more induced vertical movement. Higher arm slots also typically have greater extension. Potentially playing around with slight adjustments to the arm slot through a simple cue like “release this ball a little higher” or “On this pitch, try to get a little more downhill” could help pitchers better command the ball vertically. 
Conclusion

Finding relationships between biomech data and location is difficult for several reasons. The purpose of the bullpen is mostly unknown. Findings from command pens, velocity pens, and pitch design pens could potentially be different. Additionally, the intent of the pitcher is unknown.Would the findings be different if we knew beforehand where the athlete was aiming? Potentially. The information presented above may not offer immediate, actionable insights for coaches to apply in their training practices, but it could serve as a starting point for future studies and experiments related to command.









