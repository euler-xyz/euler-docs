# Introduction

While we eventually plan to move to a reactive interest rate model that will optimise for utilisation, we start off with a standard kink model. The kink model has different parameters for 4 main groups:

1. Majors
2. Stables
3. Mid caps
4. Small caps (default)

The parameters are:

1. Base IR (APR when utilisation is 0%)
2. Kink IR (APR when utilisation is exactly Kink%)
3. Max IR (APR when utilisation is 100%)
4. Kink% (Percent utilisation where kink occurs)

The main consideration is maintaining target utilisation (typically at Kink%).&#x20;
