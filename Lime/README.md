In \autoref{table:classification_examples} we present representative examples and the corresponding prediction of
\ourmod{} over the benchmark tests. Explaining and understanding the reason behind a model's prediction is a difficult task.
Nonetheless, there are many algorithms that attempt to give an explanation or an intuition for classifiers' decisions
\cite{adadi2018peeking}, such as \lime{} \cite{lime}. \lime{} studies the connections between keywords (tokens) 
of an input and the change in the prediction of a model once they are removed. Finally, \lime{} presents 
the probability that the keyword affected the prediction. In our case, this might indicate how \ourmod{} 
focuses on keywords and statements. Thus, in order to gain an intuition for the predicted outcome of \ourmod{},
we applied \lime{} on the four examples

The first example presents a code snippet taken from PolyBench, in which \ourmod{} managed to 
identify correctly the need for an OpenMP directive. In this example, \lime{} pinpoints the variables \emph{j}, 
\emph{POLYBENCH\_LOOP\_BOUND}, \emph{A} and \emph{y\_1} as the main contributors to the decision of the model. 
This indicates that \ourmod{} focuses on the loop variable and the arrays, as it should. The second example 
presents a snippet taken from PolyBench and contains an I/O operation, thus, there is no OpenMP directive. 
\lime{} identifies the keyword \emph{fprintf} and \emph{stderr} as the reason why the model classified the snippet without OpenMP. To verify this claim, we removed these two keywords, and \ourmod{} predicts an OpenMP directive. This probably indicates that \ourmod{} understands that these specific keywords are why there is no need for an OpenMP directive. The third example, taken from SPEC-OMP, contains an OpenMP directive that \ourmod{} fails to predict correctly. By observing \lime{}'s result, the two variables, \emph{ssize\_t} and \emph{IndexPacket}, are the main reason for its incorrect prediction. After removing both variables, \ourmod{} predicts an OpenMP directive. This might be due to the model's unfamiliarity with these keywords and how they affect the code. The fourth example, taken from PolyBench, contains an assignment into three arrays. While \ourmod{} predicts (correctly) that there should be an OpenMP directive, the example does not. As with the first example, \lime{} pinpoints the loop-variable \emph{j} and the arrays as the reason for its prediction. This further indicates that the model does focus on the correct variables while making its decision.

In summary, it appears most likely that \ourmod{} focuses on the core variables and statements in order to predict its directive. However, there are still cases in which it fails to predict correctly, possibly due to unfamiliar keywords or statements.
