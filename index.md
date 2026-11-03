**Name:** Ketan Mittal

**Email:** [k1mittal@ucsd.edu](mailto:k1mittal@ucsd.edu)

**Section:** D10 - Fusion Data Science: Databases and AI Models for Gyrokinetic Transport (industry partner: General Atomics)

**Mentors:** Igor Sfiligoi (SDSC), Jeff Candy (General Atomics), Emily Belli (General Atomics)

**1. What is the most interesting topic covered in your domain this quarter?**

The most interesting topic for me was how hard it is to simulate plasma turbulence in a nuclear fusion reactor, and how hard it is to copy those simulations with a neural network. A tokamak loses heat and particles through turbulence, so predicting that transport is key to designing and controlling a reactor. The most accurate simulations, like CGYRO, are extremely expensive, and even the faster reduced model, TGLF, is too slow for real-time use. Neural networks can make these predictions almost instantly, but training one well is really difficult. The fluxes vary wildly in size, the physics behind the inputs is complicated, and the high-fidelity data we have is very small. On top of that, a neural network has no idea where its training data ends, so it can confidently give a wrong answer. Balancing speed, accuracy, and trust in the model ended up being a really interesting problem.

**2. Describe a potential investigation you would like to pursue for your Quarter 2 Project.**

One investigation I would like to pursue is generating tens of thousands of new TGLF data points and seeing if training on them improves our surrogate's accuracy by any margin. In Quarter 1, our learning curve showed that the VAE was still improving as we gave it more data, while the linear baseline had already flattened out. This suggests our model is limited by the amount of data rather than its design. Since TGLF is cheap compared to CGYRO, running a much larger scan is realistic. I would retrain the model on larger and larger datasets, test it on the same held-out cases so the results are comparable, and see where the improvement levels off. Even if the gain is small, it would tell us how much TGLF data a surrogate like ours really needs, which is useful for anyone building one in the future. Ultimately, our goal and hope for Quarter 2 is to simulate TGLF with above 99.9% accuracy while still being over 100,000 times faster.

**3. What is a potential change you'd make to the approach taken in your current Quarter 1 Project?**

One change I would make is to expand our current neural network architectures so they fit the data better and reach a higher accuracy, even if we lose some speed. Our current model is quite small, and it is far faster than we actually need it to be. So, I would try wider and deeper networks, residual blocks like the encoder-ResNet-decoder used in the TGLF-WINN paper, and larger ensembles. The rule I would follow is that the model must still stay a handful of orders of magnitude faster than TGLF, so it remains useful for integrated modeling and reactor control. This trades a bit of our extra speed for a model that is much closer to TGLF, and it pairs well with the larger TGLF dataset from my investigation, since bigger models usually need more data.

**4. What other techniques would you be interested in using in your project?**

I would be interested in using physics-informed neural networks, or neural networks with constrained parameters, so the model follows the physics and real-life limits of a fusion plasma. Right now our model only learns from data, so nothing stops it from predicting something impossible, like a negative heat flux or an electron particle flux that doesn't match the ion flux. I would build these rules directly into the model, for example by forcing the heat fluxes to be positive and adding penalties to the loss when predictions break known physical trends. I would also keep the inputs within the ranges a real reactor can reach. This would help the model generalize better with a small amount of data and behave more sensibly outside its training range, which is exactly where our current surrogate is the least trustworthy.
