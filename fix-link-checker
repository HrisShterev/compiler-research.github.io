#!/usr/bin/env bash
set -e

echo "🔧 Running HTML-Proofer auto-fixes..."

# Target only source files (not _site)
FILES=$(grep -RIl --exclude-dir=_site --exclude-dir=.git '<img\|<a\|href=' .)

########################################
# 1. Add alt="" to <img> missing alt
########################################
echo "🖼  Fixing missing alt attributes..."
sed -i -E '
  s/<img([^>]*)(?<!alt="[^"]*")>/<img\1 alt="">/g
' $FILES

########################################
# 2. Fix <a> tags missing href
########################################
echo "Fixing <a> tags missing href..."
sed -i -E '
  s/<a([^>]*)(?![^>]*href=)/<a\1 href="#">/g
' $FILES

########################################
# 3. Fix protocol-relative URLs // → https://
########################################
echo "Fixing protocol-relative URLs..."
sed -i '
  s|="//|="https://|g
' $FILES

########################################
# 4. Upgrade http:// → https://
########################################
echo "Upgrading http:// to https://..."
sed -i '
  s|http://|https://|g
' $FILES

########################################
# 5. Normalize internal Jekyll links (/path → /path/)
########################################
echo "Normalizing internal links..."
sed -i -E '
  s|href="(/[^"#?]+)(?<!/)"|href="\1/"|g
' $FILES

########################################
# Done
########################################
echo "Auto-fixes complete."
echo "Now run: bundle exec jekyll build && htmlproofer ./_site"
