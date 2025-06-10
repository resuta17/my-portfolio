<template>
     <div class=" mb-4 text-center text-white">
        <p class=" text-xl font-semibold ">Contact Me</p>
        <p>I'm excited to work with you!</p>
      </div>
      <div class="flex flex-col justify-start items-center text-gray-900 space-y-4">
        <input
          placeholder="Name"
          class="border border-gray-300 rounded px-4 py-2 w-64 text-sm bg-white"
        />
        <input
          placeholder="Email"
          class="border border-gray-300 rounded px-4 py-2 w-64 text-sm bg-white"
        />
        <input
          placeholder="Subject"
          class="border border-gray-300 rounded px-4 py-2 w-64 text-sm bg-white"
        />
        <textarea
          placeholder="Message"
          rows="5"
          class="border border-gray-300 rounded px-4 py-2 w-64 resize-none text-sm bg-white"
        ></textarea>
        <div class="flex justify-end ">
          <button class="border border-gray-300 rounded px-4 py-2 w-64 text-white bg-gray-800 text-sm cursor-pointer">
            Submit
          </button>
        </div>
      
      </div> 
</template>

<script>

export default {
    
    
}
</script>