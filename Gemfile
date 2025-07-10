# Gemfile

source "https://rubygems.org"

# Minimal Mistakes 테마의 기본 의존성을 불러옵니다.
# (jekyll-paginate, jekyll-sitemap, jekyll-gist 등 포함)
gemspec

# Jekyll 플러그인 그룹
group :jekyll_plugins do
  # 관리자 UI 플러그인
  gem "jekyll-admin"
  
  # 태그 및 카테고리 아카이브 페이지 생성을 위한 필수 플러그인
  gem "jekyll-archives"

  gem "jekyll-seo-tag"
end

# jekyll-sitemap은 gemspec에 이미 포함되어 있지만, 
# GitHub Pages에서 명시적으로 요구할 수 있으므로 남겨두는 것이 안전합니다.
gem "jekyll-sitemap"