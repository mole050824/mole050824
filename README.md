# Hello! 👋

## 2026 Progress

<p align="center">
  <img src="https://img.shields.io/badge/Year%20Progress-127%2F365-40c463?style=for-the-badge" />
</p>

## Contribution Graph

<p align="center">
  <img src="https://ghchart.rshah.org/40c463/mole050824" width="100%" />
</p>

## GitHub Stats

<p align="center">
  <img height="170" src="https://github-readme-stats.vercel.app/api?username=mole050824&amp;show_icons=true&amp;theme=github_dark&amp;hide_border=true&amp;cache_seconds=86400" />
  <img height="170" src="https://github-readme-stats.vercel.app/api/top-langs/?username=mole050824&amp;layout=compact&amp;theme=github_dark&amp;hide_border=true&amp;cache_seconds=86400" />
</p>

---

<p align="center">
  <i>Keep going.</i>
</p>




///////


import datetime

def generate_year_progress_svg():
    now = datetime.datetime.now()
    year = now.year
    
    # 1월 1일 및 요일 계산 (파이썬은 0이 월요일이므로, 깃허브 기준인 일요일=0 으로 보정)
    jan1 = datetime.date(year, 1, 1)
    start_day_of_week = (jan1.weekday() + 1) % 7 
    
    # 윤년 확인 및 총 일수 계산
    is_leap_year = (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0)
    total_days = 366 if is_leap_year else 365
    
    # 1월 1일부터 오늘까지 지난 일수 계산
    passed_days = now.timetuple().tm_yday
    
    # SVG 기본 설정 (잔디 크기 10px, 간격 4px)
    cell_size = 10
    gap = 4
    
    svg_elements = []
    
    for i in range(total_days):
        col = (i + start_day_of_week) // 7
        row = (i + start_day_of_week) % 7
        
        x = col * (cell_size + gap)
        y = row * (cell_size + gap)
        
        # 지난 날이면 초록색, 아직 안 온 날이면 회색
        color = "#39d353" if i < passed_days else "#ebedf0"
        
        rect = f'<rect x="{x}" y="{y}" width="{cell_size}" height="{cell_size}" rx="2" ry="2" fill="{color}"></rect>'
        svg_elements.append(rect)
        
    # SVG 전체 크기 계산
    width = ((total_days + start_day_of_week) // 7 + 1) * (cell_size + gap)
    height = 7 * (cell_size + gap)
    
    # SVG 파일 내용 조합
    svg_content = f"""<svg xmlns="http://www.w3.org/2000/svg" width="{width}" height="{height}">
    {''.join(svg_elements)}
</svg>"""
    
    # 파일로 저장
    with open("year_progress.svg", "w") as f:
        f.write(svg_content)
        
    print("year_progress.svg 파일이 성공적으로 생성되었어!")

if __name__ == "__main__":
    generate_year_progress_svg()
