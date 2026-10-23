### Copy Multiple Objects from Point a1 to Point a2

```
^C^C_.select \_copy;_P;;!a1;!a2;
```

**How it Works**

1.  ^C^C_.select \ – Starts AutoCAD's native SELECT tool and pauses \ to let you pick <br />as many objects as you want (clicking individual items or dragging windows).
2.  _copy; – Once you press Enter to finish selecting, the macro immediately fires up the<br /> COPY tool.
3.  _P;; – Automatically inputs P for Previous selection, which instantly grabs all<br /> the items you just selected, and hits Enter.
4.  for Point 1 (Base point) and Point 2 (First copy destination)

**LISP Method**
```
(defun C:a (/ )
    (setq old_orthomode (getvar "orthomode"))
    '(setvar "orthomode" 1)
    (setq a1 (getpoint "\n1st point :"))
    (setq a2 (getpoint "\n2nd point :" a1))
    (setq a (distance a1 a2))
    (princ (strcat "\nDistance is " (rtos a 2 1)))
    (setvar "orthomode" old_orthomode)
    (princ)
) ;_ end of defun
(defun c:CP0 () (command "_.select" pause) (command "._copy" "_P" "" a1 a2))
```
### abbott-cancel - Esc
```
^C^C^C(sssetfirst nil)
```
### abbott-mee - F4
```
m2p
```
### abbott-TK - F1
```
tk
```
