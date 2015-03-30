# Final Project Assignment 2: Exploration (FP2) 
DUE March 30, 2015 Wednesday (2015-03-30)

### Program Code:
```
#lang racket

(require racket/draw)
(require racket/gui)

;path element for node box
(define node_path_target (make-bitmap 31 16))
(define node_path_dc (new bitmap-dc% [bitmap node_path_target]))
(define node-path
  (let ([p (new dc-path%)])
    (send p move-to 0 0)
    (send p line-to 30 0)
    (send p line-to 30 15)
    (send p line-to 0 15)
    (send p move-to 15 0)
    (send p line-to 15 15)
    (send p close)
    p))

(define (paint-node dc)
  (send node_path_dc draw-path node-path)
  (make-object image-snip% node_path_target))


;path element for terminal node box
(define terminal_node_path_target (make-bitmap 31 16))
(define terminal_node_path_dc (new bitmap-dc% [bitmap terminal_node_path_target]))
(define terminal-node-path
  (let ([p (new dc-path%)])
    (send p move-to 0 0)
    (send p line-to 30 0)
    (send p line-to 30 15)
    (send p line-to 0 15)
    (send p move-to 15 0)
    (send p line-to 15 15)
    (send p move-to 15 0)
    (send p line-to 30 15)
    (send p close)
    p))

(define (paint-terminal-node dc)
  (send terminal_node_path_dc draw-path terminal-node-path)
  (make-object image-snip% terminal_node_path_target))


;path element for data box
(define data_path_target (make-bitmap 16 16))
(define data_path_dc (new bitmap-dc% [bitmap data_path_target]))
(define data-path
  (let ([p (new dc-path%)])
    (send p move-to 0 0)
    (send p line-to 15 0)
    (send p line-to 15 15)
    (send p line-to 0 15)
    (send p line-to 0 0)
    (send p close)
    p))

(define (paint-data dc)
  (send data_path_dc draw-path data-path)
  (make-object image-snip% data_path_target))


;path element for down arrow
(define down_arrow_path_target (make-bitmap 11 31))
(define down_arrow_path_dc (new bitmap-dc% [bitmap down_arrow_path_target]))
(define down-arrow-path
  (let ([p (new dc-path%)])
    (send p move-to 5 0)
    (send p line-to 5 30)
    (send p move-to 5 30)
    (send p line-to 10 20)
    (send p move-to 5 30)
    (send p line-to 0 20)
    (send p close)
    p))

(define (paint-down-arrow dc)
  (send down_arrow_path_dc draw-path down-arrow-path)
  (make-object image-snip% down_arrow_path_target))


;path element for the right arrow
(define right_arrow_path_target (make-bitmap 31 11))
(define right_arrow_path_dc (new bitmap-dc% [bitmap right_arrow_path_target]))
(define right-arrow-path
  (let ([p (new dc-path%)])
    (send p move-to 0 5)
    (send p line-to 30 5)
    (send p move-to 30 5)
    (send p line-to 20 10)
    (send p move-to 30 5)
    (send p line-to 20 0)
    (send p close)
    p))

(define (paint-right-arrow dc)
  (send right_arrow_path_dc draw-path right-arrow-path)
  (make-object image-snip% right_arrow_path_target))


;path element for the final list
(define list_path_target (make-bitmap 100 100))
(define list_path_dc (new bitmap-dc% [bitmap list_path_target]))
(define list-path
  (let ([p (new dc-path%)])
    (send p move-to 0 0)
    (send p append node-path)
    (send p close)
    p))

(define (paint-list dc)
  (send list_path_dc draw-path list-path)
  (send list_path_dc draw-path down-arrow-path 2 7)
  (send list_path_dc draw-path right-arrow-path 23 2)
  (send list_path_dc draw-path data-path 0 38)
  (send list_path_dc draw-path terminal-node-path 54 0)
  (send list_path_dc draw-path down-arrow-path 56 7)
  (send list_path_dc draw-path data-path 54 38)
  (make-object image-snip% list_path_target))
```

### My Library: Racket Drawing Toolkit
### Narrative:
The code I wrote creates a number of dc-paths. The first few are the building blocks that I can use to create larger and more complex lists. These include node-path, terminal-node-path, data-path, down-arrow-path, and right-arrow-path. These can be combined to create list-path, although I will have to do more research into how to do this dynamically. I'm thinking I might be able to create a procedure to use with tree-map so it will iterate over a tree/list and create the appropriate structure.

As I said in the FP1 narrative, my intent with this setup is to build a tool to display lists and trees graphically and provide editing capabilities. In order to do this, I need to be able to add editable text fields dynamically as well. I hope to add two ways of viewing the data, one for pure lists and one for trees. The tree view will display elements using diagonal arrows rather than using down-arrow-path and right-arrow-path. I'd like to be able to add different colors to the different levels, but that would be a stretch-goal.

### Program Output/Images:
https://drive.google.com/folderview?id=0B7j4TU2jQ5KxREJWSmNpM25KdG8&usp=sharing
