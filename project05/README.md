# Introduction

Description of the project

# Pseudocode

## Smith-Waterman Algorithm

```         
Initialize score and traceback matrices (2 matrices total)
  m <- number of rows is length seq1 (known as i) + 1
  n <- number of columns is length seq2 (known as j) + 1
  set matrix values to 0



For i from 1 to m:
  For j from 1 to n:
    score_matrix[i,j], traceback_matrix[i, j] <- Call on score matrix function

Find the highest score in the matrix and its position

return Call traceback function, score_matrix
```

## Scoring Matrix

````         
Function cal_score(matrix, seq1, seq2, i, j, match, mismatch, gap)
  ```
  Args:
        matrix (numpy array): scoring matrix
        seq1 (str): sequence 1
        seq2 (str): sequence 2
        i (int): current row number
        j (int): current column number
  ```
  
  diag_node <- [i-1, j-1]
  left_node <- [i, j-1]
  up_node <- [i-1, j]
  
  diag_score <- if nucleotide in i and j match (using seq1 and seq2): diag_node + match/mismatch
  left_score <- left_node + gap
  up_score <- upper_node + gap
  
  score <- max(0, diag_score, up_score, left_score)
  
  if score == diag_score:
    traceback = 1
  elif score == up_score:
    traceback = 2
  elif score == left_score:
    traceback = 3
  else:
    traceback = 0
    
  return score, traceback 
  
  
````

## Traceback

````         
Function traceback(seq1, seq2, traceback_matrix, maximum_position)
  ```
  Args:
      seq1 (str) : First sequence being aligned
      seq2 (str) : Second sequence being aligned
      traceback_matrix (numpy array): traceback matrix
      maximum_position (tuple): starting position to trace back from
        
  Returns:
      aligned_seq1 (str): e.g. GTTGAC
      aligned_seq2 (str): e.g. GTT-AC
  ```
  Initialize aligned_seq1 and aligned_seq2 as strings
  current_move <- traceback_matrix at maximum_position
  
  current_row, current_column <- maximum_position
  
  While current_move is not 0 (END)
    if current_move == 1 (DIAG) 
        concatenate nucleotide (seq1[current_row]) to aligned_seq1
        concatenate nucleotide (seq2[current_column]) to aligned_seq2
        current_move <- traceback_matrix at position (current_row-1, current_column-1)
    elif current_move == 2 (UP)
        concatenate nucleotide (seq1[current_row]) to aligned_seq1
        concatenate "-" to aligned_seq2
        current_move <- traceback_matrix at position (current_row-1, current_column)
    elif current_move == 3 (LEFT)
        concatenate "-" to aligned_seq1
        concatenate nucleotide (seq2[current_column]) to aligned_seq2
        current_move <- traceback_matrix at position (current_row, current_column-1)
    
  return aligned_seq1, aligned_seq2
    
        
  
````

# Successes

-   We learned to use and handle np.arrays.

# Struggles

-   Determining which sequences correlated with the rows and columns of the matrix.

# Personal Reflections

## Group Leader - Jason

Group leader's reflection on the project

## Other member - Zoe

This project became much more manageable once we understood how the scoring and traceback processes in the alignment graph worked. However, since we were both relatively new to working with NumPy arrays, we had to look up specific functions to achieve our intended outcomes. Although we clearly understood the purpose of each function, the `traceback()` function required special attention. We needed to ensure that the rows and columns of the matrices correlated to the correct sequences. Using `print()` statements throughout the program was especially helpful for debugging and visualizing the program’s behavior. We then removed these statements to produce a clean and polished final submission.

# Generative AI Appendix

As per the syllabus
