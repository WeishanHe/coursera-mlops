# Overview of the ML Lifecycle and Deployment


![[Pasted image 20220703113456.png]]

## Week 1: The Machine Learning Project Lifecycle
![[Pasted image 20220703114641.png]]

![[Pasted image 20220703115045.png]]

## Deployment
- Two Key Challenges
	- statistical issues
		Concept drift and Data drift: What if your data changes after your system has already been deployed? The term data drift is used to describe if the input distribution x changes. The term concept drift refers to change in the desired mapping from x to y changed.
	- software engineering issues
		- Realtime or Batch prediction
		- Cloud vs. Edge/Browser
		- Compute resources (CPU/GPU/memory)
		- Latency, throughput (QPS): Throughput refers to how many queries per second do you need to handle given your compute resources given a certain number of Cloud Service.
		- Logging
		- Security and privacy
	- First deployment vs. maintenance
		- common deployment cases
			1. New product/capability
			2. Automate/assist with manual task
			3. Replace previous ML system
		- key ideas:
			- Gradual ramp up with monitoring: rather than sending tons of traffic to a not fully proven learning algorithm, you may send only a small amount of traffic and monitor it and then ramp up the percentage or amount of traffic
			- Rollback: if the algorithm isn't working, you can revert back to the previous system if indeed there was an earlier system.
- Deployment Patterns
	- Shadow model deployment: 
		- ML system shadows the human and runs in parallel. 
		- ML system's output not used for any decisions during this phase.
	- Canary deployment: 
		- Roll out to small fraction (say 5%) of traffic initially
		- Monitor system and ramp up traffic gradually 
	- Blue green deployment 
		- Have the router send images to the old/blue version to make decisions first. And then stop sending images to the old one and switch over the the new/green version.
		- The advantage of this deployment is that there's an easy way to enable rollback
	- Deployment Framework - Degree of automation
	Human only $\rightarrow$ Shadow mode $\rightarrow$ AI assistance $\rightarrow$ Partial automation $\rightarrow$ Full automation
		- You can choose to stop before getting to full automation. 
		- AI assistance and Partial automation also refer to human in the loop deployment

## Monitoring
- Monitoring dashboard: 
	- Brainstorm the thins that could go wrong
	- Brainstorm a few statistics/metrics that will detect the problem
	- It is ok to use many metrics initially and gradually remove the ones you find not useful
	- Examples of metrics to track
		- software metrics: memory, compute, latency, throughput, server load
		- statistical/performance metrics
			- input metrics: avg input length, avg input volume, num of missing values, avg image brightness
			- output metrics: # times return null, # times user redoes search, # times user switches to typing, CTR
	- Set thresholds for alarms
	- Adapt metrics and thresholds over time
- Model maintenance
	- Manual retraining
	- Automatic retraining
## Pipeline monitoring
- Metrics to monitor: 
	- Monitor: software metrics, input metrics, output metrics
	- How quickly do they change?
		- user data generally has slower drift
		- enterprise data (B2B applications) can shift fast

## Week 1 Optional References
**Week 1: Overview of the ML Lifecycle and Deployment**
If you wish to dive more deeply into the topics covered this week, feel free to check out these optional references. You won’t have to read these to complete this week’s practice quizzes.

[Concept and Data Drift](https://towardsdatascience.com/machine-learning-in-production-why-you-should-care-about-data-and-concept-drift-d96d0bc907fb)

[Monitoring ML Models](https://christophergs.com/machine%20learning/2020/03/14/how-to-monitor-machine-learning-models/)

[A Chat with Andrew on MLOps: From Model-centric to Data-centric](https://youtu.be/06-AZXmwHjo)

**Papers**

Konstantinos, Katsiapis, Karmarkar, A., Altay, A., Zaks, A., Polyzotis, N., … Li, Z. (2020). Towards ML Engineering: A brief history of TensorFlow Extended (TFX). [http://arxiv.org/abs/2010.02013](http://arxiv.org/abs/2010.02013) 

Paleyes, A., Urma, R.-G., & Lawrence, N. D. (2020). Challenges in deploying machine learning: A survey of case studies. [http://arxiv.org/abs/2011.09926](http://arxiv.org/abs/2011.09926)

Sculley, D., Holt, G., Golovin, D., Davydov, E., & Phillips, T. (n.d.). Hidden technical debt in machine learning systems. Retrieved April 28, 2021, from Nips.c [https://papers.nips.cc/paper/2015/file/86df7dcfd896fcaf2674f757a2463eba-Paper.pdf](https://papers.nips.cc/paper/2015/file/86df7dcfd896fcaf2674f757a2463eba-Paper.pdf)

