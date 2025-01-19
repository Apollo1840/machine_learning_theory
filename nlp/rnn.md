# RNN
reference:
- https://onedrive.live.com/edit.aspx?resid=BEF76BD482A6B496!16288&migratedtospo=true&wd=target%28%E6%B7%B1%E5%BA%A6%E5%AD%A6%E4%B9%A0-%E8%87%AA%E7%84%B6%E8%AF%AD%E8%A8%80%E5%A4%84%E7%90%86.one%7C41c92d6c-9e88-49b8-a90d-6f642459dfe3%2FRNN%7C162e9bf2-163c-4ae0-bb01-06020061276d%2F%29&wdorigin=NavigationUrl


Recurrent Neural Networks (RNNs) are designed to handle sequential data by maintaining a **hidden state** that captures information about previous elements in the sequence. It is updated at each time step based on the **current** input and the **previous** hidden state.

## seq2seq

Seq2seq (sequence-to-sequence) problems involve mapping an input sequence to an output sequence, which can **vary** in length.

In a seq2seq problem, RNN could use the previous output as the current input to generate sequences until a certain output is obtained.


## Advance RNN
GRU and LSTM enhance the vanilla RNN by introducing gated mechanisms to 
- handle **long-term** dependencies
- **stabilize** training
- provide more **flexibility** 
  in processing sequence data.



