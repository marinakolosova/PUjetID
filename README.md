# Pileup JetID

This branch contains the weights for pileup jetid for 2017 UL (106X) data for AK4 CHS jets. These weights:

1. they are trained in eta bins [0, 2.5], [2.5, 2.75], [2.75, 3.0], [3.0, 5.0] different from previously shared recipe (2016 data).
2. New working points are derived in 4 pT bins [10, 20], [20, 30], [30, 40], and [40, 50].
3. instead of using id flags use `mva` value to apply cut/id.


## Instructions to download weights

```
git clone -b 106X_weights_2017UL git@github.com:cms-jet/PUjetID.git PUJetIDweights/
cp PUJetIDWeights/weights/pileupJetId_UL17_Eta* $CMSSW_BASE/src/RecoJets/JetProducers/data/
rm -rf PUJetIDweights/  ### If needed
```

## Changes in CMSSW

 * For 102X: `git cms-merge-topic alefisico:PUID_102X`
 * For 106X: `git cms-merge-topic alefisico:PUID_106X`

## Changes in config file
 
```
from RecoJets.JetProducers.PileupJetID_cfi import _chsalgos_94x, _chsalgos_102x, _chsalgos_106X_UL17
process.load(“RecoJets.JetProducers.PileupJetID_cfi”)
process.pileupJetId.jets = cms.InputTag(“ ... ”)
process.pileupJetId.inputIsCorrected = True
process.pileupJetId.applyJec = False
process.pileupJetId.vertexes = cms.InputTag(“offlineSlimmedPrimaryVertices”)
process.pileupJetId.algos = cms.VPSet(_chsalgos_)
```

## Scale Factors and uncertainties

In the folder ScaleFactors, root files containing the scale factors and uncertainties are included. 

   * LINK TO UL17 SFs: contains efficiencies, mistag rates, and uncertainties for 2017 UL samples using the 106X training.
