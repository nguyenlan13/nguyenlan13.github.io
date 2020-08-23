---
layout: post
title:      "Boolean Short Circuit"
date:       2020-08-23 23:12:16 +0000
permalink:  boolean_short_circuit
---


Boolean Short Circuit

Short circuit evaluation with boolean operators is evaluating the second argument only if the first argument does not satisfy the truthiness or falsiness of the expression. Using the operator “&&” would require that both sides of the operator be truthy, if the left hand side is falsey, it will short circuit and not evaluate the right hand side.

```
Def test(one, two)
   If one && two
       puts “is true”
       return one && two
   else
	     puts “is false”
	     return one && two
   end
end
```

Using the “||” operator, if the left hand side of the operator is truthy, then the right hand side will not be evaluated.

```
Def test(one, two)
   If one || two
       puts “is true”
       return one || two
   else
	     puts “is false”
	     return one || two
    end
end
```

