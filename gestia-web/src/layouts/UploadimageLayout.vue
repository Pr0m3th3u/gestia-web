
<template>
    <div class="common-layout">
      <el-container>

        <el-header class="header">
            <slot name="header">HEADER</slot>
        </el-header>

        <el-main>
          <div class="content">
            <slot />
          </div>
          <div class="actions">
            <slot name="buttons"></slot>
          </div>
        </el-main>
        
      </el-container>
    </div>
  </template>
  
  <script>
  export default {
    name: "CommonLayout",
  };
  import '../style.css'
  </script>
  
  <style>

  .common-layout {
    border: 1px solid #ccc;
    padding: 10px;
    margin: auto;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    background-color: var(--background-color);
  }
  
  .content {
    margin: 0 auto;
    padding: 10px;
  }

  .header {
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--subtle-text-color);
    font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    font-weight: 700;
  }

  .actions {
    display: flex;
    justify-content: flex-end;
    margin-top: 10px;
  }
  
  .actions > * {
    margin-left: 10px;
  }
  </style>
  