# Introduction

While we eventually plan to move to a reactive interest rate model that will optimise for utilisation, we start off with a standard kink model. The parameters of our kink model are:

1. Base IR (APY when utilisation is 0%)
2. Kink IR (APY when utilisation is exactly Kink%)
3. Max IR (APY when utilisation is 100%)
4. Kink% (Percent utilisation where kink occurs)

The main consideration is maintaining target utilisation (typically at Kink%).&#x20;
