# Neural Network Basics
reference: https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28ML.one%7Ce8b3e705-493c-431b-b04e-8e9e3752864d%2F07-NeuroNetwork%7C02a354b1-68be-4afe-ac68-241c18b29aab%2F%29&wdorigin=NavigationUrl


## losses
- mse
- entropy
    - binary cross-entropy
    - categorical cross-entropy
- focal loss
- triplenet loss
- similarity loss

## Advances

### Normalization
- Batch normalization
- Layer normalization
- Instance normalization
- group normalization

### Dropout

Randomly deactivate a fraction of neurons of a layer whenever tensor pass forward during the training phase.

It prevents the network from becoming overly reliant on specific neurons, thus promoting the learning of more robust and general features and reducing overfitting.

### Skip connection
Skip connection is a concept used in neural networks. It allows the model to bypass one or more layers by feeding the output of one layer directly into another layer further down the network.
- ( <-- ) It provides shorter paths for gradients to flow through the network, maintaining stronger gradients for early layers, and facilitating deeper deep learning.
- ( --> ) on the other hand, it allows the model to leverage both shallow and deep representations of the data, hence benefiting the performance and accelerating training in some cases.
