
• Case sensitive naming
• Variable names have to start with letters or _

• Line joing by \, but no comments behind \
if 1900 < year < 2100 and 1 <= month <= 12 \
and 1 <= day <= 31 and 0 <= hour < 24 \
and 0 <= minute < 60: # only here are comments allowed
• But better:
if (1900 < year < 2100 and 1 <= month <= 12
and 1 <= day <= 31 and 0 <= hour < 24 # comment here
and 0 <= minute < 60): # and here are comments allowed


