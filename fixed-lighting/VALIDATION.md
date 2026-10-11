# Validation — 2026-10-11

WeiDU 25100 parsed the final installer successfully.

Both components were installed and uninstalled against synthetic resource
fixtures using the actual WeiDU executable. The BG1EE-only predicate was
removed only from the temporary fixture copies, because the fixtures are
not a licensed game installation.

Verified daylight flags change only for outdoor cycling areas; indoor and
non-cycling areas remain unchanged. Full byte comparisons verify every
unrelated byte is preserved.

Verified native night copies contain the intended original resource bytes,
unique six-character names work across counter 9 to 10, the ARE WED reference
is correctly expanded and zero-padded, missing resources leave their areas
unchanged, and original shared WED/BMP resources remain intact.

Verified WeiDU uninstall restores the original area bytes and removes the
private night resources in both fixture runs.

Not verified: live BG1EE installation, game detection, packaged DLC access,
native renderer behavior, transitions, effect expiry inside BG1EE, or existing
save compatibility. Those require the in-game checks in README.md.
