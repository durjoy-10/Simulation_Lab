# CIT 324 Simulation Lab: Lab 1–20 বাংলা Explanation

এই নোটে প্রতিটি Lab-এর code দেওয়া হয়নি। এখানে শুধু প্রতিটি Lab-এর কাজ, logic, step-by-step ব্যাখ্যা, output-এর meaning, এবং graph কী বুঝায়—এসব সহজ বাংলায় লেখা হয়েছে।

---

## Lab 1: M/M/1 Queue Simulation

### Problem idea
এই Lab-এ একটি single-server queue system simulate করা হয়। Customer random সময় পরপর আসে, server একজন, এবং service time-ও random। শেষে average delay in queue, average number in queue, server utilization, এবং simulation ending time বের করা হয়।

### Step-by-step logic
প্রথমে simulation clock শূন্য থেকে শুরু করা হয়। Server কখন free হবে সেটাও শুরুতে শূন্য ধরা হয়। প্রতিটি customer-এর জন্য interarrival time generate করা হয়, অর্থাৎ আগের customer-এর পর নতুন customer কত সময় পরে আসবে। তারপর service time generate করা হয়, অর্থাৎ customer-এর service শেষ করতে কত সময় লাগবে।

Customer arrival time বের করার জন্য current clock-এর সাথে interarrival time যোগ করা হয়। এরপর দেখা হয় server free কিনা। যদি customer arrival time server free time-এর পরে হয়, তাহলে customer সাথে সাথে service পাবে। আর যদি server busy থাকে, তাহলে customer wait করবে এবং service শুরু হবে server free হওয়ার পরে।

Delay in queue হলো service start time থেকে arrival time বাদ দিলে যা পাওয়া যায়। প্রতিটি customer-এর delay যোগ করে total delay পাওয়া যায়। Server যতক্ষণ service দেয়, সেই service times যোগ করলে busy time পাওয়া যায়। শেষ customer service শেষ করার সময়ই simulation ending time।

### Output meaning
Average delay in queue দেখায় একজন customer গড়ে কতক্ষণ queue-তে wait করেছে। Average number in queue Little’s Law দিয়ে বের করা হয়: arrival rate × average delay। Server utilization দেখায় মোট simulation time-এর কত অংশ server busy ছিল। Time simulation ended হলো শেষ customer system থেকে বের হওয়ার সময়।

### Graph explanation
Delay graph-এ x-axis customer number এবং y-axis delay in queue। এতে বোঝা যায় কোন customer বেশি wait করেছে। Arrival-departure graph থাকলে বোঝা যায় customer কখন system-এ এসেছে এবং কখন বের হয়েছে।

---

## Lab 2: Inventory Management Simulation

### Problem idea
এই Lab-এ একটি দোকান বা warehouse-এর stock system simulate করা হয়। প্রতিদিন demand হয়, stock কমে, stock কমে reorder point-এর নিচে গেলে নতুন order করা হয়।

### Step-by-step logic
শুরুতে initial stock নেওয়া হয়। প্রতিদিন random demand generate করা হয়। যদি stock demand-এর চেয়ে বেশি বা সমান হয়, তাহলে পুরো demand পূরণ হয় এবং stock কমে যায়। যদি demand stock-এর চেয়ে বেশি হয়, তাহলে যত stock আছে তত বিক্রি হয় এবং বাকি অংশ shortage হিসেবে ধরা হয়।

প্রতিদিনের শেষে stock reorder point-এর নিচে নেমেছে কিনা দেখা হয়। যদি stock reorder point বা তার নিচে থাকে, তাহলে নির্দিষ্ট order quantity যোগ করা হয়। এভাবে প্রতিদিনের stock level, demand, shortage, এবং order quantity track করা হয়।

### Output meaning
Total sales দেখায় মোট কত unit বিক্রি হয়েছে। Total shortage দেখায় মোট কত demand পূরণ করা যায়নি। Total order quantity দেখায় মোট কত stock reorder করা হয়েছে। Ending stock দেখায় simulation শেষে stock কত আছে।

### Graph explanation
Stock level graph দেখায় প্রতিদিন stock কীভাবে কমেছে এবং reorder হলে আবার বেড়েছে। Demand graph প্রতিদিনের demand দেখায়। Shortage graph কোন দিনে shortage হয়েছে তা দেখায়। Order graph কোন দিনে reorder হয়েছে তা বুঝায়।

---

## Lab 3: Continuous Review Inventory System

### Problem idea
এই Lab-এ continuous review inventory system বা (s, S) policy simulate করা হয়। Stock প্রতিদিন check করা হয়। Stock s level-এর নিচে গেলে order দিয়ে stock S level পর্যন্ত পূরণ করা হয়।

### Step-by-step logic
শুরুতে initial stock নেওয়া হয়। প্রতিদিনের demand normal distribution থেকে generate করা হয়, কারণ real-life demand সাধারণত average demand-এর আশেপাশে ওঠানামা করে। Demand negative হলে সেটি শূন্য ধরা হয়। এরপর stock demand পূরণ করতে পারে কিনা দেখা হয়। Stock যথেষ্ট হলে stock কমে যায়, shortage হয় না। Stock কম হলে shortage তৈরি হয় এবং stock শূন্য হয়।

তারপর holding cost এবং shortage cost হিসাব করা হয়। Holding cost হলো বাকি stock ধরে রাখার খরচ। Shortage cost হলো demand পূরণ না হওয়ার penalty। তারপর reorder rule apply করা হয়। Stock যদি s বা তার নিচে হয়, তাহলে stock S পর্যন্ত পূরণ করার জন্য order দেওয়া হয়।

### Output meaning
Total holding cost দেখায় পুরো simulation-এ stock ধরে রাখার মোট cost। Total shortage cost দেখায় shortage-এর জন্য মোট penalty। Total cost হলো holding cost এবং shortage cost-এর যোগফল। Total shortage দেখায় মোট কত unit demand পূরণ হয়নি।

### Graph explanation
Stock level graph দেখায় inventory কখন কমেছে এবং reorder হলে কখন বেড়েছে। Demand graph demand variation দেখায়। Shortage cost graph shortage হওয়ার কারণে cost কেমন হয়েছে দেখায়। Holding cost বনাম shortage cost graph cost comparison দেখায়।

---

## Lab 4: Bernoulli Distribution

### Problem idea
এই Lab-এ একটি chip pass বা fail করবে—এই দুই outcome নিয়ে Bernoulli distribution দেখানো হয়। Pass হলে value 1, fail হলে value 0 ধরা হয়।

### Step-by-step logic
প্রথমে pass probability p ধরা হয়। Fail probability হয় 1 − p। Bernoulli distribution-এ mean সরাসরি p হয় এবং variance হয় p(1 − p)। এই values calculate করে output দেখানো হয়।

### Output meaning
Pass probability দেখায় chip ভালো হওয়ার সম্ভাবনা। Fail বা defect probability দেখায় chip defective হওয়ার সম্ভাবনা। Mean হলো expected success value। Variance দেখায় outcome কতটা spread করতে পারে।

### Graph explanation
Bar chart-এ দুইটি bar থাকে: Fail এবং Pass। Pass probability বেশি হলে pass bar উঁচু হবে।

---

## Lab 5: Network Packet Delivery

### Problem idea
এই Lab-এ network packet delivery Binomial distribution দিয়ে model করা হয়। মোট 15টি packet পাঠানো হয় এবং প্রতিটি packet success হওয়ার probability 0.90। Exactly 13 packets successful হওয়ার probability বের করা হয়।

### Step-by-step logic
মোট trial n = 15। Success probability p = 0.90। Failure probability q = 1 − p। Exactly 13 success-এর probability binomial formula দিয়ে বের করা হয়। Mean হয় n × p এবং variance হয় n × p × q। Observed data থাকলে তার sample average-ও বের করা হয়।

### Output meaning
Exactly 13 packet arrive করার probability দেখায় 15টির মধ্যে ঠিক 13টি packet successful হওয়ার সম্ভাবনা। Mean দেখায় expected successful packet সংখ্যা। Variance দেখায় successful packet সংখ্যার variation। Sample average observed result-এর average দেখায়।

### Graph explanation
Bar chart-এ 0 থেকে 15 পর্যন্ত successful packet সংখ্যা দেখানো হয়। যেহেতু success probability বেশি, তাই 13, 14, 15 এর bar সাধারণত বেশি হয়।

---

## Lab 6: Poisson Distribution

### Problem idea
এই Lab-এ call center-এ প্রতি ঘণ্টায় average 5টি call আসার ঘটনাকে Poisson distribution দিয়ে model করা হয়। 0 থেকে 10 call আসার probability বের করা হয়।

### Step-by-step logic
Poisson distribution ব্যবহার করা হয় যখন নির্দিষ্ট সময়ের মধ্যে কোনো event কতবার ঘটবে তা model করতে হয়। এখানে event হলো call arrival। Average rate λ = 5। প্রতিটি k value-এর জন্য probability বের করা হয়। Poisson distribution-এ mean এবং variance দুটোই λ।

### Output meaning
P(X = 0), P(X = 1), ..., P(X = 10) দেখায় এক ঘণ্টায় নির্দিষ্ট সংখ্যক call আসার probability। Mean = 5 মানে average 5টি call আসে। Variance = 5 মানে call arrival variability-ও 5।

### Graph explanation
Bar chart-এ number of calls x-axis এবং probability y-axis। Highest bar সাধারণত 4 বা 5 call-এর আশেপাশে থাকে।

---

## Lab 7: Normal Distribution

### Problem idea
এই Lab-এ normal distribution-এর unimodal এবং multimodal density curve দেখানো হয়। Mean 100 এবং standard deviation 20 সহ sample size 200 generate করা হয়। এছাড়া men-এর diastolic blood pressure mean 80 এবং standard deviation 20 ধরে histogram দেখানো হয়।

### Step-by-step logic
প্রথমে একটি normal density curve তৈরি করা হয় যেখানে একটি peak থাকে। এটিই unimodal distribution। এরপর দুইটি normal distribution mix করে multimodal curve তৈরি করা হয়, যেখানে একাধিক peak দেখা যায়। তারপর mean 100, SD 20, sample size 200 দিয়ে random sample generate করা হয়। Blood pressure example-এর জন্য mean 80 এবং SD 20 দিয়ে আরেকটি sample generate করা হয়।

### Output meaning
Sample mean দেখায় generated data-এর average। Sample standard deviation দেখায় data mean থেকে কতটা ছড়ানো। Blood pressure sample mean ও SD দেখায় simulated blood pressure data-এর characteristics।

### Graph explanation
Unimodal graph-এ একটি bell-shaped peak থাকে। Multimodal graph-এ একাধিক peak থাকে। Histogram bell shape হলে বোঝা যায় data normal distribution follow করছে। Blood pressure histogram-ও যদি bell-shaped হয়, তাহলে সেটি normal distribution-এর সাথে মানানসই।

---

## Lab 8: Exponential Distribution

### Problem idea
এই Lab-এ COVID wave-এর waiting time exponential distribution দিয়ে model করা হয়। যদি average 100 দিনে একটি wave হয়, তাহলে next wave 120 দিনের বেশি পরে আসার probability বের করা হয়। পাশাপাশি λ = 0.5, 1.0, 2.0, 4.0 দিয়ে exponential curves simulate করা হয়।

### Step-by-step logic
Average time 100 দিন হলে rate parameter λ = 1/100। Exponential distribution-এর survival probability ব্যবহার করে P(X > 120) বের করা হয়। এরপর বিভিন্ন rate parameter দিয়ে exponential density curve আঁকা হয়। λ যত বড় হয়, curve তত দ্রুত নিচে নামে, কারণ event দ্রুত ঘটার সম্ভাবনা বেশি।

### Output meaning
P(next wave takes more than 120 days) দেখায় একটি wave-এর পর next wave আসতে 120 দিনের বেশি লাগার probability। যদি value প্রায় 0.30 হয়, তাহলে probability প্রায় 30%।

### Graph explanation
COVID waiting time graph দেখায় waiting time যত বাড়ে probability density কমে যায়। Rate comparison graph-এ বড় λ-এর curve দ্রুত decay করে।

---

## Lab 9: Empirical Input Modeling

### Problem idea
এই Lab-এ customer arrival time-এর raw dataset-কে theoretical distribution-এর সাথে fit করা হয়। Normal, Weibull এবং Lognormal distribution ব্যবহার করা হয়। Parameter estimate করা হয় Maximum Likelihood Estimation বা MLE দিয়ে। Fit validate করা হয় Q-Q plot দিয়ে।

### Step-by-step logic
প্রথমে raw data array হিসেবে নেওয়া হয়। Normal distribution fit করলে mean এবং standard deviation estimate হয়। Weibull distribution fit করলে shape, location এবং scale parameter estimate হয়। Lognormal distribution fit করলেও shape, location এবং scale পাওয়া যায়। এগুলো MLE method দিয়ে estimate করা হয়।

এরপর histogram-এর উপর fitted distribution-এর density curve বসানো হয়। তারপর Q-Q plot তৈরি করা হয়। যদি Q-Q plot-এর points straight line-এর কাছাকাছি থাকে, তাহলে distribution fit ভালো।

### Output meaning
Estimated parameters দেখায় কোন distribution data-এর সাথে কীভাবে fit হয়েছে। Normal-এর mean ও SD data-এর central tendency ও spread দেখায়। Weibull ও Lognormal-এর shape/scale parameters data-এর distribution shape বুঝায়।

### Graph explanation
Histogram with fitted curve দেখায় theoretical distribution raw data-এর সাথে কতটা মিলে। Q-Q plot fit validation করে। Points line-এর কাছাকাছি থাকলে fit ভালো।

---

## Lab 10: Machine Breakdown and Maintenance

### Problem idea
এই Lab-এ 5টি identical machine simulate করা হয়। Breakdown-এর মধ্যবর্তী সময় exponential distribution follow করে এবং repair time Weibull distribution follow করে। প্রতিটি machine-এর downtime এবং overall system throughput calculate করা হয়।

### Step-by-step logic
প্রতিটি machine-এর জন্য আলাদা clock চলে। Machine কিছু সময় কাজ করে, তারপর breakdown হয়। Breakdown হওয়ার সময় পর্যন্ত machine uptime পায়। Breakdown হলে repair time generate করা হয়। Repair time-টাই downtime হিসেবে যোগ হয়। Repair শেষে machine আবার কাজ শুরু করে। এই process simulation time শেষ হওয়া পর্যন্ত চলে।

প্রতিটি machine-এর total downtime, uptime, breakdown count এবং throughput বের করা হয়। Throughput সাধারণত uptime × production rate ধরা হয়।

### Output meaning
Machine downtime দেখায় কোন machine কতক্ষণ বন্ধ ছিল। Total system downtime সব machine-এর downtime-এর যোগফল। Uptime দেখায় machine কতক্ষণ কাজ করেছে। Overall throughput দেখায় system মোট কত output produce করেছে।

### Graph explanation
Downtime bar chart machine-wise downtime compare করে। Breakdown count graph কোন machine কতবার breakdown হয়েছে দেখায়। Throughput graph কোন machine বেশি production দিয়েছে দেখায়। Uptime-downtime stacked graph total time breakdown করে।

---

## Lab 11: Linear Congruential Generator (LCG)

### Problem idea
এই Lab-এ LCG method দিয়ে pseudo-random number generate করা হয়। LCG হলো random number generation-এর একটি basic deterministic method।

### Step-by-step logic
LCG formula হলো next value = current value, multiplier, increment এবং modulus দিয়ে calculate করা। শুরুতে seed value নেওয়া হয়। প্রতিবার formula apply করে নতুন value পাওয়া যায়। এরপর value-কে modulus দিয়ে ভাগ করে 0 থেকে 1 এর মধ্যে pseudo-random number বানানো হয়। এই process n বার repeat করা হয়।

### Output meaning
Generated number list pseudo-random sequence দেখায়। যেহেতু এই method deterministic, একই seed ও parameter দিলে একই sequence পাওয়া যায়। Modulus ছোট হলে sequence দ্রুত repeat করতে পারে।

### Graph explanation
Line graph-এ generated random numbers-এর sequence দেখায়। Value 0 থেকে 1-এর মধ্যে ওঠানামা করে। Repeat pattern দেখা গেলে বোঝা যায় modulus বা parameter ছোট।

---

## Lab 12: Random Variates Using Inverse Transform Function

### Problem idea
এই Lab-এ inverse transform method ব্যবহার করে exponential distribution-এর random variates generate করা হয়। Uniform random number থেকে desired distribution-এর random value তৈরি করা হয়।

### Step-by-step logic
প্রথমে 0 থেকে 1-এর মধ্যে uniform random numbers generate করা হয়। Exponential distribution-এর inverse CDF formula ব্যবহার করে এই uniform numbers-কে exponential random variates-এ convert করা হয়। Rate parameter λ দিয়ে values control করা হয়।

### Output meaning
First 10 random variates দেখায় generated exponential values-এর কিছু sample। এগুলো exponential distribution follow করে। λ বড় হলে generated values সাধারণত ছোট হয়।

### Graph explanation
Histogram right-skewed হয়। ছোট values বেশি দেখা যায় এবং বড় values কম দেখা যায়। এটি exponential distribution-এর natural shape।

---

## Lab 13: Exponential Random Numbers with Theoretical PDF

### Problem idea
এই Lab-এ inverse transform technique দিয়ে 5000টি exponentially distributed random number generate করা হয়। তারপর histogram-এর উপর theoretical exponential PDF overlay করা হয়।

### Step-by-step logic
প্রথমে 5000 uniform random numbers generate করা হয়। inverse transform formula দিয়ে সেগুলো exponential data-তে convert করা হয়। এরপর theoretical exponential PDF calculate করা হয়। Generated data-এর histogram আঁকা হয় এবং তার উপর theoretical curve বসানো হয়।

### Output meaning
Generated data sample exponential distribution থেকে এসেছে কিনা তা histogram ও PDF curve দেখে বোঝা যায়। Histogram এবং theoretical curve কাছাকাছি হলে generation method ঠিক।

### Graph explanation
Histogram generated values-এর empirical distribution দেখায়। Curve theoretical exponential distribution দেখায়। দুইটি closely match করলে model valid।

---

## Lab 14: Debugging and Traceability Verification

### Problem idea
এই Lab-এ একটি simple discrete-event queue model trace করা হয়। প্রতিটি event-এর পর system state print করা হয় যেন logical rules ঠিক আছে কিনা দেখা যায়।

### Step-by-step logic
Simulation clock শূন্য থেকে শুরু হয়। Queue length শূন্য থাকে। প্রতিটি event random ভাবে Arrival বা Departure হয়। Arrival হলে queue এক বাড়ে। Departure হলে queue এক কমে, কিন্তু queue শূন্য হলে আর কমানো হয় না। এতে queue কখনো negative হয় না। প্রতিটি event-এর time, type এবং queue length log করা হয়।

### Output meaning
Trace output দেখায় event number, event time, event type এবং queue length। এটি debugging-এর জন্য useful, কারণ প্রতিটি step দেখা যায়।

### Graph explanation
Step graph event number অনুযায়ী queue length দেখায়। Discrete-event simulation-এ state event অনুযায়ী পরিবর্তন হয়, তাই step graph উপযুক্ত।

---

## Lab 15: Confidence Interval Estimation

### Problem idea
এই Lab-এ M/M/1 queue simulation multiple independent replications চালিয়ে average waiting time-এর 95% confidence interval বের করা হয়। Updated version-এ sample data থেকে mean interarrival time এবং mean service time বের করে simulation input হিসেবে ব্যবহার করা হয়।

### Step-by-step logic
প্রথমে observed interarrival time data এবং service time data নেওয়া হয়। এই data থেকে mean interarrival time এবং mean service time calculate করা হয়। এরপর একটি M/M/1 simulation function তৈরি করা হয়। প্রতিটি replication-এ 100 customer simulate হয় এবং average waiting time return করা হয়।

Simulation 30 বার independent replication হিসেবে চালানো হয়। প্রতিটি replication-এর average waiting time list-এ রাখা হয়। এরপর replication means থেকে overall mean, standard error, এবং t-distribution ব্যবহার করে 95% confidence interval বের করা হয়।

### Output meaning
Mean waiting time দেখায় 30 replication-এর average result। Standard error result-এর uncertainty দেখায়। 95% confidence interval দেখায় true mean waiting time কোন range-এ থাকতে পারে।

### Graph explanation
Histogram replication-wise average waiting time-এর spread দেখায়। Histogram বেশি spread হলে uncertainty বেশি।

---

## Lab 16: Steady-State Analysis

### Problem idea
এই Lab-এ non-terminating simulation-এর warm-up period বাদ দিয়ে steady-state mean বের করা হয়। Continuous manufacturing line-এর মতো system শুরুতে unstable থাকে, পরে steady হয়।

### Step-by-step logic
প্রথমে 200 time unit-এর system response generate করা হয়। Response formula এমনভাবে করা হয় যাতে শুরুতে value বেশি থাকে এবং সময়ের সাথে steady level-এর দিকে যায়। Random noise যোগ করা হয় যেন real system-এর variation দেখা যায়।

প্রথম 50 time unit warm-up period হিসেবে বাদ দেওয়া হয়। এরপর বাকি data steady-state data হিসেবে নেওয়া হয়। এই steady-state data-এর mean calculate করা হয়।

### Output meaning
Steady-state mean দেখায় warm-up period বাদ দেওয়ার পর system response-এর average value। এটি initial bias ছাড়া বেশি reliable result দেয়।

### Graph explanation
Line graph system response over time দেখায়। Vertical dashed line warm-up cutoff দেখায়। Line-এর বাম পাশে warm-up period এবং ডান পাশে steady-state period।

---

## Lab 17: Bank ATM System Simulation

### Problem idea
এই Lab-এ একটি ATM vestibule simulate করা হয় যেখানে customers random সময় পরপর আসে, available ATM ব্যবহার করে, এবং চলে যায়। Updated version-এ sample data থেকে mean interarrival time এবং mean ATM service time বের করা হয়।

### Step-by-step logic
প্রথমে observed interarrival time data এবং ATM service time data থেকে mean calculate করা হয়। Simulation-এ 100 customer এবং 3 ATM machine ধরা হয়। প্রতিটি ATM কখন free হবে তা list-এ রাখা হয়। প্রতিটি customer-এর arrival time exponential distribution দিয়ে generate করা হয়, যেখানে mean আসে sample data থেকে। Service time-ও sample data-derived mean দিয়ে generate হয়।

Customer আসার পর সবচেয়ে আগে free হবে এমন ATM select করা হয়। যদি selected ATM customer arrival time-এর পর free হয়, তাহলে customer wait করে। Wait করলে queue length হিসাব করা হয়। যদি ATM free থাকে, waiting time শূন্য হয়। শেষে ATM-এর free time update করা হয়।

### Output meaning
Maximum queue length দেখায় simulation-এর মধ্যে সর্বোচ্চ queue pressure কত ছিল। Average waiting time দেখায় customer গড়ে কতক্ষণ wait করেছে।

### Graph explanation
Queue length graph customer অনুযায়ী queue size দেখায়। Waiting time graph দেখায় কোন customer কতক্ষণ wait করেছে।

---

## Lab 18: Fast-Food Drive-Thru Model

### Problem idea
এই Lab-এ fast-food drive-thru process simulate করা হয়। Stage তিনটি: order, pay, pickup। Updated version-এ sample data থেকে mean order time, mean pay time, এবং mean pickup time বের করা হয়।

### Step-by-step logic
প্রথমে order, pay এবং pickup stage-এর observed sample data নেওয়া হয়। প্রত্যেক data list থেকে mean calculate করা হয়। এরপর 100 car simulate করা হয়। প্রতিটি car-এর জন্য order time, pay time এবং pickup time exponential distribution দিয়ে generate করা হয়, যেখানে mean values sample data থেকে পাওয়া।

প্রতিটি stage-এর simulated average time বের করা হয়। তারপর সবচেয়ে বেশি average time যেই stage-এর, সেটি bottleneck হিসেবে identify করা হয়।

### Output meaning
Mean order/pay/pickup time from data দেখায় observed data-এর average। Simulation results দেখায় simulated average stage times। Bottleneck stage দেখায় system-এর সবচেয়ে slow অংশ।

### Graph explanation
Bar chart order, pay এবং pickup stage-এর average time compare করে। Highest bar bottleneck নির্দেশ করে।

---

## Lab 19: Emergency Room Patient Flow

### Problem idea
এই Lab-এ ER patient flow simulate করা হয়। Stage তিনটি: triage, treatment, discharge। Updated version-এ sample data থেকে mean triage time, mean treatment time, এবং mean discharge time বের করা হয়।

### Step-by-step logic
প্রথমে triage, treatment এবং discharge time-এর sample observed data নেওয়া হয়। প্রতিটি list থেকে mean calculate করা হয়। তারপর 100 patient simulate করা হয়। প্রতিটি patient-এর triage, treatment এবং discharge time exponential distribution দিয়ে generate করা হয়।

একজন patient-এর total time হলো triage + treatment + discharge। সব patient-এর জন্য stage-wise times এবং total times store করা হয়। এরপর average triage time, average treatment time, average discharge time এবং average total patient time বের করা হয়। সবচেয়ে বেশি average time যেই stage-এ, সেটি bottleneck।

### Output meaning
Mean values from data দেখায় real/observed data-এর average। Average total patient time দেখায় একজন patient ER system-এ গড়ে কত সময় কাটায়। Bottleneck stage দেখায় resource allocation কোথায় বেশি দরকার।

### Graph explanation
Stage-wise bar chart triage, treatment ও discharge time compare করে। Total time graph প্রতিটি patient-এর total system time দেখায়।

---

## Lab 20: Statistical Output Analysis and Precision Estimation

### Problem idea
এই Lab-এ drive-thru pharmacy simulation-এর পাঁচটি independent replication output ব্যবহার করে statistical output analysis করা হয়। Given average waiting times: 3.2, 4.3, 5.1, 4.2, 4.6 minutes।

### Step-by-step logic
প্রথমে replication waiting times data হিসেবে নেওয়া হয়। Data থেকে sample mean বের করা হয়, যা point estimate। Sample variance বের করা হয় result কতটা spread করেছে তা বোঝার জন্য। Sample standard deviation এবং standard error calculate করা হয়।

যেহেতু replication সংখ্যা কম, Student’s t-distribution ব্যবহার করে 95% confidence interval তৈরি করা হয়। Confidence interval-এর half-width বের করা হয়। Desired half-width 0.5 minutes হলে approximate formula দিয়ে required number of replications বের করা হয়।

### Output meaning
Sample mean হলো overall point estimate। Sample variance stochastic variability দেখায়। Standard error mean estimate-এর uncertainty দেখায়। 95% confidence interval true mean waiting time-এর likely range দেয়। Required replications দেখায় desired precision পেতে কত simulation run দরকার।

### Graph explanation
Replication line graph প্রতিটি replication-এর waiting time দেখায়। Bar chart waiting time compare করে এবং sample mean line দেখায়। এতে বোঝা যায় কোন replication mean-এর উপরে বা নিচে।

---

# Final Note

Simulation lab exam-এ প্রতিটি problem-এর জন্য সাধারণ structure হলো: problem বুঝা, input বা sample data নেওয়া, mean বা parameter calculate করা, simulation logic apply করা, output বের করা, এবং graph দিয়ে result explain করা। Code মুখস্থ করার চেয়ে logic বুঝলে exam-এ সহজে লিখতে পারবে।
