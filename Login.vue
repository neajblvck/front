<template>

	<div v-if="!authenticated">
		<h2>Authentification</h2>
		<form @submit.prevent="login">
			<label>
			Email:
			<input type="email" v-model="email" required autocomplete="username">
			</label>
			<label>
			Mot de passe:
			<input type="password" v-model="password" required autocomplete="current-password">
			</label>
			<button type="submit">Se connecter</button>
		</form>
	</div>

	<div v-else>
		<h2>Bienvenue {{ userName }}</h2>
		<button @click="logout">Se déconnecter</button>
	</div>

</template>


<script>

import {accountService} from '@/services'

export default {
	name: 'login',
	data() {
	  return {
		email: '',
		password: '',
		userName: '',
		userId: null,
		authenticated: false
	  };
	},
	created() {
	  const token = sessionStorage.getItem('token');
	  if (token) {
		this.getUser(token);
	  }
	},
	methods: {
		login() {
		const credentials = {
		    email: encodeURIComponent(this.email),
  			password: encodeURIComponent(this.password)
		};
		
		fetch(BASE_URL+'/api/auth/login', {
		  method: 'POST',
		  headers: {
			'Content-Type': 'application/json'
		  },
		  body: JSON.stringify(credentials)
		})
		  .then(res => {
			if (!res.ok) {
			  throw new Error('Authentification échouée');
			}
			return res.json();
		  })
		  .then(data => {
			const token = data.token;
			sessionStorage.setItem('token', data.token);
			this.getUser(data.token);
		  })
		  .catch(error => {
			console.log(error);
		  });
	  },
	  
	  getUser(token) {
		fetch('http://localhost:3000/api/auth', {
		  method: 'GET',
		  headers: {
			'Authorization': `Bearer ${token}`
		  }
		})
		  .then(res => {
			if (!res.ok) {
			  throw new Error('Impossible de récupérer l\'utilisateur');
			}
			return res.json();
		  })
		  .then(data => {
			this.userId = data.userId;
			this.userName = data.userName;
			this.authenticated = true;
			this.$router.push('admin/dashboard')
			console.log(data)
		  })
		  .catch(error => {
			console.log(error);
		  });
	  },
	  logout() {
		sessionStorage.removeItem('token');
		this.userName = null;
		this.authenticated = false;
	  }
	}
  };
</script>

<style scoped>
</style>