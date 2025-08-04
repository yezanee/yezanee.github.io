---
title: TIL
icon: fas fa-graduation-cap
order: 2
---

> **Today I Learned** - 오늘 배운 것들을 정리하는 공간입니다.
{: .prompt-info }

<br>

<div class="calendar-container">
  <div class="calendar-header">
    <button id="prevMonth" class="calendar-btn">&lt;</button>
    <h3 id="currentMonth">2025년 8월</h3>
    <button id="nextMonth" class="calendar-btn">&gt;</button>
  </div>

  <table class="calendar-table">
    <thead>
      <tr>
        <th>일</th>
        <th>월</th>
        <th>화</th>
        <th>수</th>
        <th>목</th>
        <th>금</th>
        <th>토</th>
      </tr>
    </thead>
    <tbody id="calendarBody">
      <!-- JavaScript로 동적 생성 -->
    </tbody>
  </table>
</div>

<style>
.calendar-container {
  max-width: 800px;
  margin: 30px auto;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  background: #ffffff;
  border-radius: 16px;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
  padding: 25px;
  border: 1px solid #e1e5e9;
}

.calendar-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 25px;
  padding-bottom: 20px;
  border-bottom: 2px solid #e1e5e9;
}

.calendar-header h3 {
  font-size: 24px;
  font-weight: 600;
  color: #2c3e50;
  margin: 0;
  letter-spacing: -0.5px;
}

.calendar-btn {
  background: #87ceeb;
  color: white;
  border: none;
  padding: 12px 18px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 16px;
  font-weight: 500;
  transition: all 0.2s ease;
}

.calendar-btn:hover {
  background: #5f9ea0;
  transform: translateY(-1px);
}

.calendar-btn:disabled {
  background: #d1d5db;
  cursor: not-allowed;
  transform: none;
}

.calendar-table {
  width: 100%;
  border-collapse: separate;
  border-spacing: 0;
  background: #ffffff;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  border: 1px solid #e1e5e9;
}

.calendar-table th {
  background: #f8f9fa;
  padding: 18px 15px;
  text-align: center;
  font-weight: 600;
  font-size: 14px;
  color: #495057;
  border-bottom: 2px solid #e9ecef;
  letter-spacing: 0.5px;
}

.calendar-table td {
  padding: 18px 15px;
  text-align: center;
  border: 1px solid #f1f3f4;
  cursor: pointer;
  transition: all 0.2s ease;
  font-weight: 500;
  font-size: 15px;
  color: #2c3e50;
  position: relative;
}

.calendar-table td:hover {
  background: #f8f9fa;
  transform: scale(1.02);
}

.calendar-table td.has-til {
  background: #e0f6ff;
  font-weight: 600;
  color: #2c5aa0;
  border: 2px solid #87ceeb;
}

.calendar-table td.has-til:hover {
  background: #b3e0ff;
  transform: scale(1.05);
}

.calendar-table td.has-til a {
  color: #2c5aa0;
  text-decoration: none;
  font-weight: 600;
  display: block;
  width: 100%;
  height: 100%;
}

.calendar-table td.has-til a:hover {
  color: #1e3a8a;
}

.calendar-table td.other-month {
  color: #bdc3c7;
  background: #fafbfc;
}

.calendar-table td.today {
  background: #fff3cd;
  font-weight: 700;
  color: #856404;
  border: 2px solid #fdcb6e;
  position: relative;
}

.calendar-table td.today::after {
  content: '';
  position: absolute;
  top: 4px;
  right: 4px;
  width: 8px;
  height: 8px;
  background: #f39c12;
  border-radius: 50%;
}

@media (max-width: 768px) {
  .calendar-container {
    margin: 15px;
    padding: 20px;
  }
  
  .calendar-header h3 {
    font-size: 20px;
  }
  
  .calendar-table td {
    padding: 12px 8px;
    font-size: 14px;
  }
  
  .calendar-table th {
    padding: 15px 8px;
    font-size: 13px;
  }
}
</style>

<script>
// 배포 환경에서 JavaScript 실행 문제 해결
(function() {
  'use strict';
  
  // 전역 변수로 초기화 상태 추적
  let calendarInitialized = false;
  
  function initCalendar() {
    if (calendarInitialized) {
      console.log('캘린더가 이미 초기화됨');
      return;
    }
    
    console.log('initCalendar 함수 실행됨');
    
    // TIL 게시물 데이터 - 실제 _posts 폴더의 TIL 게시물들과 연동
    const tilPosts = {
      '2025-08-04': {
        title: 'TIL - 2025년 8월 4일',
        url: '/posts/til-250804/',
      }
    };

    // 최소 날짜 설정 (2025년 8월 1일)
    const MIN_DATE = new Date(2025, 7, 1); // 2025년 8월 1일

    let currentDate = new Date(2025, 7, 1); // 2025년 8월 1일

    function updateCalendar() {
      console.log('updateCalendar 함수 실행됨');
      
      const year = currentDate.getFullYear();
      const month = currentDate.getMonth();
      
      const monthElement = document.getElementById('currentMonth');
      console.log('monthElement:', monthElement);
      
      if (monthElement) {
        monthElement.textContent = `${year}년 ${month + 1}월`;
      }
      
      // 이전 월 버튼 비활성화/활성화
      const prevBtn = document.getElementById('prevMonth');
      console.log('prevBtn:', prevBtn);
      
      if (prevBtn) {
        const isMinDate = currentDate.getFullYear() === MIN_DATE.getFullYear() && 
                         currentDate.getMonth() === MIN_DATE.getMonth();
        prevBtn.disabled = isMinDate;
      }
      
      const firstDay = new Date(year, month, 1);
      const lastDay = new Date(year, month + 1, 0);
      const startDate = new Date(firstDay);
      startDate.setDate(startDate.getDate() - firstDay.getDay());
      
      const calendarBody = document.getElementById('calendarBody');
      console.log('calendarBody:', calendarBody);
      
      if (!calendarBody) {
        console.error('Calendar body element not found');
        return;
      }
      
      calendarBody.innerHTML = '';
      
      const today = new Date();
      
      for (let week = 0; week < 6; week++) {
        const row = document.createElement('tr');
        
        for (let day = 0; day < 7; day++) {
          const cell = document.createElement('td');
          const currentDate = new Date(startDate);
          currentDate.setDate(startDate.getDate() + week * 7 + day);
          
          const dateString = currentDate.toISOString().split('T')[0];
          const dayNumber = currentDate.getDate();
          
          // 오늘 날짜 체크
          const isToday = currentDate.toDateString() === today.toDateString();
          // 현재 월이 아닌 날짜 체크
          const isOtherMonth = currentDate.getMonth() !== month;
          // TIL 게시물이 있는 날짜 체크
          const hasTil = tilPosts[dateString];
          
          if (isOtherMonth) {
            cell.className = 'other-month';
            cell.textContent = dayNumber;
          } else if (hasTil) {
            cell.className = 'has-til';
            cell.innerHTML = `<a href="${hasTil.url}" title="${hasTil.title}">${dayNumber}</a>`;
          } else {
            cell.textContent = dayNumber;
          }
          
          if (isToday) {
            cell.classList.add('today');
          }
          
          row.appendChild(cell);
        }
        
        calendarBody.appendChild(row);
      }
      
      console.log('캘린더 업데이트 완료');
      calendarInitialized = true;
    }

    // 이벤트 리스너
    const prevBtn = document.getElementById('prevMonth');
    if (prevBtn) {
      prevBtn.addEventListener('click', () => {
        const newDate = new Date(currentDate);
        newDate.setMonth(newDate.getMonth() - 1);
        
        // 최소 날짜보다 이전으로 이동하려고 하면 무시
        if (newDate >= MIN_DATE) {
          currentDate = newDate;
          updateCalendar();
        }
      });
    }

    const nextBtn = document.getElementById('nextMonth');
    if (nextBtn) {
      nextBtn.addEventListener('click', () => {
        currentDate.setMonth(currentDate.getMonth() + 1);
        updateCalendar();
      });
    }

    // 초기화
    updateCalendar();
  }

  // 여러 방법으로 실행 시도
  console.log('스크립트 로드됨, DOM 상태:', document.readyState);

  // 즉시 실행 시도
  if (document.readyState === 'loading') {
    console.log('DOM 로딩 중, DOMContentLoaded 이벤트 등록');
    document.addEventListener('DOMContentLoaded', initCalendar);
  } else {
    console.log('DOM 이미 로드됨, 즉시 실행');
    initCalendar();
  }

  // 추가 안전장치: window.onload
  window.addEventListener('load', function() {
    console.log('window.onload 실행됨');
    // DOM이 완전히 로드되었지만 캘린더가 아직 초기화되지 않은 경우
    const calendarBody = document.getElementById('calendarBody');
    if (calendarBody && calendarBody.children.length === 0) {
      console.log('캘린더가 비어있음, 재초기화');
      initCalendar();
    }
  });

  // 지연 실행 시도들
  setTimeout(function() {
    console.log('setTimeout 100ms로 지연 실행 시도');
    initCalendar();
  }, 100);

  setTimeout(function() {
    console.log('setTimeout 500ms로 지연 실행 시도');
    initCalendar();
  }, 500);

  setTimeout(function() {
    console.log('setTimeout 1000ms로 지연 실행 시도');
    initCalendar();
  }, 1000);

  // requestAnimationFrame을 사용한 추가 시도
  if (typeof requestAnimationFrame !== 'undefined') {
    requestAnimationFrame(function() {
      console.log('requestAnimationFrame으로 실행 시도');
      initCalendar();
    });
  }

})();
</script>