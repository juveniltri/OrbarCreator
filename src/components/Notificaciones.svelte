<script>
    export let message = '';
    export let type = 'info';
  </script>
  
  <div class={`notification ${type}`}>
    {message}
  </div>
  
  <style>
    .notification {
      position: fixed;
      top: 20px;
      left: 50%;
      transform: translateX(-50%);
      z-index: 10;
      padding: 1em;
      color: #fff;
      border-radius: 10px;
    }
    .error {
      background-color: red;
    }
    .info {
      background-color: blue;
    }
  </style>
  