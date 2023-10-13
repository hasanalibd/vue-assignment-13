<script setup>
import { ref, computed, watch } from 'vue';

const user = ref({
  name: 'John Doe',
  profileImage: 'https://media.licdn.com/dms/image/C4E03AQGJOYQ9kZo1aQ/profile-displayphoto-shrink_800_800/0/1615767680630?e=2147483647&v=beta&t=Fmon9XRgNTKxNSATOW1Ch7je1ieyDByns-hwUQeeD8Q',
  birthdate: '',
  email: 'example@gmail.com',
  description: 'write something about yourself',
});

const birthYear = computed(() => {
  if (user.value.birthdate) {
    const birthdate = new Date(user.value.birthdate);
    return birthdate.getFullYear();
  }
  return '';
});

const votingEligibilityMessage = computed(() => {
  if (user.value.birthdate) {
    const birthdate = new Date(user.value.birthdate);
    const age = new Date().getFullYear() - birthdate.getFullYear();
    return age >= 18 ? 'Eligible for voting' : 'Not eligible for voting';
  }
  return '';
});
const userAgeClass = computed(() => {
  return {
    'bg-success': user.value.birthdate && new Date().getFullYear() - new Date(user.value.birthdate).getFullYear() >= 18,
    'bg-danger': user.value.birthdate && new Date().getFullYear() - new Date(user.value.birthdate).getFullYear() < 18,
  };
});
watch(user, (newUser, oldUser) => {
  if (newUser.birthdate !== oldUser.birthdate) {
    user.value.birthYear = birthYear.value;
    user.value.votingEligibilityMessage = votingEligibilityMessage.value;
  }
});
</script>


<template>
  <div class="container mt-4">
    <div class="row">
      <div class="col-md-4">
        <div class="card text-center bg-success mt-2" :class="userAgeClass">
          <div class="card-body">
            <div>
              <img :src="user.profileImage" alt="" width="340" class="img-thumbnail">
            </div>
            <div>
              <h3>Name: {{ user.name }}</h3>
            </div>
            <div>
              <h3>Birth Year: {{ birthYear }}</h3>
            </div>

            <div>
              <h2>{{ votingEligibilityMessage }}</h2>
            </div>
          </div>
        </div>
      </div>
      <div class="col-md-8">
        <div class="card">
          <div class="card-header">
            <h4>User Profile</h4>
          </div>
          <div class="card-body">
            <h2 class="text-center">User Details</h2>

            <div class="row mb-3 align-items-center">
              <div class="col-md-3 text-end">
                <label for="name" class="col-form-label">Name</label>
              </div>
              <div class="col-md-7">
                <input type="text" id="name" class="form-control" v-model="user.name">
              </div>
            </div>
            <div class="row mb-3 align-items-center">
              <div class="col-md-3 text-end">
                <label for="img" class="col-form-label">Image</label>
              </div>
              <div class="col-md-7">
                <input type="text" id="img" class="form-control" v-model="user.profileImage" placeholder="Input image linke here">
              </div>
            </div>
            <div class="row mb-3 align-items-center">
              <div class="col-md-3 text-end">
                <label for="dob" class="col-form-label">Birth Date</label>
              </div>
              <div class="col-md-7">
                <input type="date" id="dob" class="form-control" v-model="user.birthdate">
              </div>
            </div>
            <div class="row mb-3 align-items-center">
              <div class="col-md-3 text-end">
                <label for="email" class="col-form-label">Email</label>
              </div>
              <div class="col-md-7">
                <input type="email" id="email" class="form-control" v-model="user.email">
              </div>
            </div>
            <div class="row mb-3 align-items-center">
              <div class="col-md-3 text-end">
                <label for="description" class="col-form-label">Description</label>
              </div>
              <div class="col-md-7">
                <textarea id="description" v-model="user.description" class="form-control"></textarea>
              </div>
            </div>
          
          </div>
        </div>
      </div>
    </div>
    
  </div>
</template>


