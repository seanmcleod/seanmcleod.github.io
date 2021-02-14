---
title: "Landing - Ground Effect, Flare - JSBSim"
date: 2018-02-06T00:36:03+02:00
---

Taking a look at the ground effect and the flare on landing performance using JSBSim to 
see it's effect on the final sink rate and the change in airspeed.

For this test I'm using the Boeing 737 model included with JSBSim. The aircraft is setup 
and trimmed at 150ft AGL with a speed of 140kt IAS and on a 3 degree flight path with 
the flaps and gear down.

This is the Cl versus AoA for the B-737 model.

![image alt text](/images/landing-ground-effect-flare-jsbsim/b737clvsalpha.png)

The coefficient of induced drag versus AoA. It increases as the square of the AoA.

![image alt text](/images/landing-ground-effect-flare-jsbsim/b737cdivsalpha.png)

The ground effect kicks in when the aircraft is roughly within 1 wingspan above the ground. 
For the B-737 this means the ground effect starts at just under 100ft AGL since it has a 
wingspan of 93ft.

There are two main changes in aircraft performance when in ground effect, namely the 
coefficient of lift (Cl) increases for a given angle of attack and the induced drag coefficient 
decreases for a given angle of attack. Both effects increase the closer the aircraft gets to 
the ground, expressed as the ratio b/h (wingspan / AGL).

The following graph shows the increase in Cl versus b/h as a factor increase over the normal 
Cl versus AoA used for this B-737 model.

![image alt text](/images/landing-ground-effect-flare-jsbsim/b737clfactorvshb.png)

So at an AGL of 50ft there is a roughly 2% increase in the coefficient of lift which rises to 
roughly 6% at 25ft AGL.

The following graph shows the decrease in the induced drag coefficient Cdi versus b/h.

![image alt text](/images/landing-ground-effect-flare-jsbsim/b737cdifactorvshb.png)

At an AGL of 50ft there is roughly a 7% decrease in induced drag and when we get down to 25ft AGL 
there is roughly a 24% decrease.

So left unchecked during the landing the ground effect will result in a slight 'float' down the 
runway in terms of the extra lift being generated and with lower induced drag and the increased lift 
will lower the sink rate.

Three landing tests were performed, all with the same starting conditions, i.e. trimmed at 140kt IAS 
at 150ft AGL with a flight path angle of 3 degrees resulting in a descent rate of 12.5ft/s or 750fpm.

In the 1st landing test the ground effects were removed from the aircraft model and no control inputs 
to the elevator or throttles were made, i.e. the aircraft continued descending at 140kts and at 750fpm 
until it hit the runway very hard.

In the 2nd landing test the ground effects were enabled but again no control inputs were made. In other 
words no pilot inputs after the control positions were set during the initial trim, but the aircraft was 
influenced by the ground effect as it descended below 100ft AGL.

In the 3rd landing test the ground effect model was enabled and the throttles were retarded at 50ft AGL 
and then the aircraft was rotated slowly in pitch in order to flare the aircraft.

> First the background: Airbus gives 3 landing distance tables, "manual/manual", "manual/autobrake" (FCOM 2.03) 
> and "autoland/autobrake".

> "Manual/manual" is the minimum landing distance based on certification flight tests. You arrive over the "screen" 
> (50ft) with Vref (Vls), retard the thrust and rotate the aircraft along a constant flight path resulting in a 
> touchdown speed of Vls minus 7-8 kts and a relatively high pitch attitude. Derotation is positive and max brakes 
> are applied without reverse.

The following graph shows the flight path for the 3 landings.

![image alt text](/images/landing-ground-effect-flare-jsbsim/b737landingprofiles.png)

And a zoomed in view from 50ft AGL onwards.

![image alt text](/images/landing-ground-effect-flare-jsbsim/b737landingprofileszoomed.png)

The landing with no ground effect and no pilot inputs followed the 3 degree flight path onto the runway, landing 
850m on from the 150ft AGL start. The landing with the ground effect enabled but with no pilot inputs ballooned above 
the initial 3 degree flight path and landed 992m from the start. The 3rd landing with pilot inputs to retard the
 engines to idle thrust and to initiate a flare landed 988m from the start.

The following graph shows the throttle and elevator inputs that were applied plus the resulting pitch rate.

![image alt text](/images/landing-ground-effect-flare-jsbsim/b737controlinputs.png)

You can see a nose pitch down rate as the engines are retarded to idle thrust just before the elevator input is applied.

As expected for the no ground effect and no pilot input landing the pitch, alpha (AoA) and gamma (flight path angle) 
all remain constant from their initial trim angles all the way onto the ground.

![image alt text](/images/landing-ground-effect-flare-jsbsim/b737alphapitchgammnoge.png)

For the ground effect landing with no pilot inputs the pitch attitude remains pretty constant around 2.4 degrees 
nose up, but as the ground effect comes into play the AoA and flight path angle decrease together as a result 
of the increased lift.

![image alt text](/images/landing-ground-effect-flare-jsbsim/b737alphapitchgammgenoinputs.png)

And lastly for the landing with pilot inputs. The flare maneuver is obvious with the increasing alpha from 
the trim value around 5.2 degrees to a peak of around 6.2 degrees which then decays back down to roughly 
5 degrees on touch down. The pitch attitude increases from 2.25 degrees to 4.75 degrees and then is held at 
this angle for approximately 1.5 seconds until touch down.

The flare also decreases the flight path angle from the initial 3 degrees to about 0.3 degrees on landing.

![image alt text](/images/landing-ground-effect-flare-jsbsim/b737alphapitchgammgewithinputs.png)

In terms of the airspeed in the no ground effect with no pilot input case the IAS remained pretty constant 
around the initial trim value of 139.5kt. In the case of the landing with ground effect and no pilot inputs 
the IAS increased by roughly 1kt in the last 4.5 seconds.

The combination of retarding the thrust to idle and increasing alpha during the flare means we bled off 
approximately 7.5kts from the initial approach speed.

![image alt text](/images/landing-ground-effect-flare-jsbsim/b737ias.png)

And lastly in terms of the descent rate during the approach and the final sink rate as the aircraft lands. 
In the landing with ground effect and no pilot inputs the ground effect decreases the final sink rate from 
750fpm down to 175fpm.

In the landing with pilot inputs to decrease the thrust and to flare the aircraft the final sink rate is 
reduced to only 75fpm, quite a greaser!

![image alt text](/images/landing-ground-effect-flare-jsbsim/b737descentrate.png)

One effect that hasn't been modeled is the change in pitch moment due to ground effect. When coming into 
ground effect the downwash angle from the wing over the tailplane is reduced which in turn reduces the 
amount of lift from the tailplane resulting in a nose down pitching moment.

Here is an example of some wind tunnel data and flight test data for the Comet airliner with a wingspan 
of 107ft and the change in pitching moment when in ground effect.

![image alt text](/images/landing-ground-effect-flare-jsbsim/groundeffectpitchingmoment.png)

If this change in pitching moment had been modelled then for the test flight with ground effect but no 
pilot input we would've seen the pitch attitude decreasing as the aircraft came into ground effect 
instead of the constant pitch attitude. This would also have changed the AoA experienced etc. For the 
test flight with pilot input we would need to apply a greater elevator deflection during the flare to 
counteract the nose down pitching moment if we wanted to achieve the same pitch attitude and AoA.