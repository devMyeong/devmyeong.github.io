---
title:  "Unreal Engine C++ The Ultimate Shooter Course (5)"

categories:
  - Unreal Engine
tags:
  - []

comments: true

toc: true
toc_sticky: true

date: 2022-12-13
last_modified_at: 2023-01-25
---

## Chapter 12 Download Footsteps Assets

### 12-230 Download Footsteps Assets
- finish

### 12-231 Setup Assets for Footsteps

![check](https://user-images.githubusercontent.com/80055816/214517597-630aeb41-4291-4afe-b547-99a5c189a55c.PNG){: width="100%" height="100%"}{: .align-center}

![mat](https://user-images.githubusercontent.com/80055816/214517671-536d431f-167e-41fd-b906-5b6743020934.PNG){: width="100%" height="100%"}{: .align-center}

### 12-232 Define Physical Surface Types

![surface](https://user-images.githubusercontent.com/80055816/214520243-f5bbae46-aa27-4bd8-84db-68408ba8e587.PNG){: width="100%" height="100%"}{: .align-center}

```cpp
// shooter.h
#define EPS_Metal EPhysicalSurface::SurfaceType1
#define EPS_Stone EPhysicalSurface::SurfaceType2
#define EPS_Tile EPhysicalSurface::SurfaceType3
#define EPS_Grass EPhysicalSurface::SurfaceType4
#define EPS_Water EPhysicalSurface::SurfaceType5
```

### 12-233 Creating Physical Materials

![phy](https://user-images.githubusercontent.com/80055816/214529078-cedee02c-fd28-460a-9dfc-9de5b66ca256.PNG){: width="100%" height="100%"}{: .align-center}

![metal](https://user-images.githubusercontent.com/80055816/214529132-2327242c-c383-4ee7-9aba-7b076a15cfce.PNG){: width="100%" height="100%"}{: .align-center}

![stone](https://user-images.githubusercontent.com/80055816/214529182-29de8e4e-0108-4ef9-b8d0-0c59b8c9d8a4.PNG){: width="100%" height="100%"}{: .align-center}

![move](https://user-images.githubusercontent.com/80055816/214529239-b2fdea65-5e00-4057-84cc-3d87f9ae793e.PNG){: width="100%" height="100%"}{: .align-center}

![grass](https://user-images.githubusercontent.com/80055816/214529281-9d9f8b6a-1a2b-47a8-8173-843dfbdcf42a.PNG){: width="100%" height="100%"}{: .align-center}

### 12-234 Footstep Sync Markers
- It has bug so in the meantime, we're going to have to wait and make do with just our trimmed animations
- If we have an animation notify to play a sound here at jog start, is that going to be played in addition to the animation notify in jog forward That's an issue
- We can solve this issue by designating one particular animation to be the leader and one particular animation to be a follower
- The leader will have its animation notifies, all triggered, whereas all followers will not have their animation notifies triggered if they're following a leader

### 12-235 Custom Anim Notify

![bp](https://user-images.githubusercontent.com/80055816/215017556-d5aa7aaf-af61-4e9f-90ab-3ae111f4b838.PNG){: width="100%" height="100%"}{: .align-center}

![notify](https://user-images.githubusercontent.com/80055816/215017673-363047e3-ea6b-444c-a0c1-86d58b74b1d2.PNG){: width="100%" height="100%"}{: .align-center}

![save](https://user-images.githubusercontent.com/80055816/215017697-85beb072-5af6-4790-9c9c-b39b2592870b.PNG){: width="100%" height="100%"}{: .align-center}

![receive](https://user-images.githubusercontent.com/80055816/215017738-9854a090-5591-4783-92c2-49218614fc73.PNG){: width="100%" height="100%"}{: .align-center}

![l](https://user-images.githubusercontent.com/80055816/215017779-2e3a215e-64df-4678-bf61-338f61a0c68c.PNG){: width="100%" height="100%"}{: .align-center}

![node](https://user-images.githubusercontent.com/80055816/215017827-14b5a9fc-fbfd-4058-902f-b87d0c790fb2.PNG){: width="100%" height="100%"}{: .align-center}

![run](https://user-images.githubusercontent.com/80055816/215017887-0b48cee0-7e9d-4803-b6de-8521a61d1109.PNG){: width="100%" height="100%"}{: .align-center}

![step](https://user-images.githubusercontent.com/80055816/215017934-c8ee451d-106b-4824-9752-e6670c252dd4.PNG){: width="100%" height="100%"}{: .align-center}

- As we see here, that's because the forward animation is designated to be the leader and the jog left animation is the follower in relation to the jog forward animation
- And so that means we won't get double footstep and notifies played at the same time

### 12-236 Adding Notifies to Animations

![noti](https://user-images.githubusercontent.com/80055816/214848138-1bf63a5d-eeff-4b42-81f1-e67dd8c8fb3d.PNG){: width="100%" height="100%"}{: .align-center}

![left](https://user-images.githubusercontent.com/80055816/214848224-df08d9f6-2f7a-45c3-a23f-935edbf61ef4.PNG){: width="100%" height="100%"}{: .align-center}

### 12-237 Setting Bone Name for Each Notify

![foot](https://user-images.githubusercontent.com/80055816/215115945-7784f111-ef1a-4e6c-bd21-9db481dcdf27.PNG){: width="100%" height="100%"}{: .align-center}

### 12-238 Playing Sounds with Anim Notify

![step](https://user-images.githubusercontent.com/80055816/215128083-8e867d3b-bd03-4f2d-b90d-5c629b57b4eb.PNG){: width="100%" height="100%"}{: .align-center}

### 12-239 Line Trace for Physical Surface Type

![reconnect](https://user-images.githubusercontent.com/80055816/215156764-de674380-cd7d-488c-bb74-2e4d0184fc57.PNG){: width="100%" height="100%"}{: .align-center}

![add](https://user-images.githubusercontent.com/80055816/215156848-d625aa0e-0951-4a5d-b350-4eebb8d28d8c.PNG){: width="100%" height="100%"}{: .align-center}

![drag](https://user-images.githubusercontent.com/80055816/215156904-f5588e8c-3b73-4207-8cbc-e14fff490285.PNG){: width="100%" height="100%"}{: .align-center}

### 12-240 The Grass Surface Type

![drop](https://user-images.githubusercontent.com/80055816/215257174-128c96f2-ab80-478d-972f-642026bacb91.PNG){: width="100%" height="100%"}{: .align-center}

![ran](https://user-images.githubusercontent.com/80055816/215257187-670b9522-187a-4dba-b1bd-265b487ea534.PNG){: width="100%" height="100%"}{: .align-center}

### 12-241 Get Surface Type

```cpp
// Shooter.Builds.cs

//..

// Now that we have PhysicsCore, we will be able to have the physical surface type as a function return type
PublicDependencyModuleNames.AddRange(new string[] { "Core", "CoreUObject", "Engine", "InputCore", "UMG", "PhysicsCore" });

//..
```

![noti](https://user-images.githubusercontent.com/80055816/215267833-8ade602f-b892-4b72-a59b-75511b27236b.PNG){: width="100%" height="100%"}{: .align-center}

### 12-242 Implement Footsteps Notify

![metal](https://user-images.githubusercontent.com/80055816/215273273-15f0944e-b781-4dce-8955-9ec85a45c41f.PNG){: width="100%" height="100%"}{: .align-center}

![ran](https://user-images.githubusercontent.com/80055816/215273281-dedbcd5a-88dd-4cb0-abee-2239f0346755.PNG){: width="100%" height="100%"}{: .align-center}

![step](https://user-images.githubusercontent.com/80055816/215273292-d69fb45a-7360-4d14-be4f-6edb32008784.PNG){: width="100%" height="100%"}{: .align-center}

![play](https://user-images.githubusercontent.com/80055816/215273299-23df877f-5396-4b52-8280-3887a550a447.PNG){: width="100%" height="100%"}{: .align-center}

![return](https://user-images.githubusercontent.com/80055816/215273311-d7f1cd03-ecf3-4270-9e31-8bd2b4166f5b.PNG){: width="100%" height="100%"}{: .align-center}

### 12-243 Jumping and Landing Sounds

![jump](https://user-images.githubusercontent.com/80055816/215279365-bdbf0b7c-ec0b-4690-9a0a-09cdb03f4f83.PNG){: width="100%" height="100%"}{: .align-center}

![sel](https://user-images.githubusercontent.com/80055816/215279390-1fedd528-614e-467b-bfae-54a0f76fdd20.PNG){: width="100%" height="100%"}{: .align-center}

![notify](https://user-images.githubusercontent.com/80055816/215279403-39757846-31fd-4fee-aead-4d81b434a75e.PNG){: width="100%" height="100%"}{: .align-center}

![noti](https://user-images.githubusercontent.com/80055816/215279420-1e66bc5c-d61e-4896-979c-a4212f90ac2b.PNG){: width="100%" height="100%"}{: .align-center}

![local](https://user-images.githubusercontent.com/80055816/215279433-6750da24-9955-41f7-9927-3ea52060f416.PNG){: width="100%" height="100%"}{: .align-center}

![buti](https://user-images.githubusercontent.com/80055816/215279446-c5b218f7-ed64-4067-9807-0ff4b6d64aad.PNG){: width="100%" height="100%"}{: .align-center}

![branch](https://user-images.githubusercontent.com/80055816/215279460-b447dbde-e8ee-4574-872e-cd31a810e1f0.PNG){: width="100%" height="100%"}{: .align-center}

![un](https://user-images.githubusercontent.com/80055816/215279475-0c918f08-86e2-41d5-9a6b-7d33c09f7148.PNG){: width="100%" height="100%"}{: .align-center}

### 12-244 Turning Hips While Running

![bp](https://user-images.githubusercontent.com/80055816/215338986-0ba1e705-ae7f-42c8-8263-cac9daa0722b.PNG){: width="100%" height="100%"}{: .align-center}

![ro](https://user-images.githubusercontent.com/80055816/215339011-7f305190-e7f3-47f2-a4ee-1132a2b25a3d.PNG){: width="100%" height="100%"}{: .align-center}

![normal](https://user-images.githubusercontent.com/80055816/215339023-67a90fe8-b1d7-48f4-aee5-5f500166b522.PNG){: width="100%" height="100%"}{: .align-center}

![node](https://user-images.githubusercontent.com/80055816/215339035-77deaa36-aa50-45f4-b91a-b242fee0ddb7.PNG){: width="100%" height="100%"}{: .align-center}

![ani](https://user-images.githubusercontent.com/80055816/215339076-f4e00e0f-2773-4eb3-b30e-8eb50bdf4e84.PNG){: width="100%" height="100%"}{: .align-center}

![forty](https://user-images.githubusercontent.com/80055816/215339096-afc604de-e86a-464b-9ff7-3f42cda0980e.PNG){: width="100%" height="100%"}{: .align-center}

![time](https://user-images.githubusercontent.com/80055816/215339108-289c4faf-956e-4beb-a8ae-f0a1f6abd667.PNG){: width="100%" height="100%"}{: .align-center}

### 12-245 Turn Hips While Running Backwards

![back](https://user-images.githubusercontent.com/80055816/215414379-08a96fc4-7096-4c65-b226-b2e65f019bd6.PNG){: width="100%" height="100%"}{: .align-center}

![temp](https://user-images.githubusercontent.com/80055816/215414423-b9d56b6e-fb71-404a-8ea7-e5c03ec42ea4.PNG){: width="100%" height="100%"}{: .align-center}

![space](https://user-images.githubusercontent.com/80055816/215414465-1f90faf5-d72a-4617-b23a-8e84706170bd.PNG){: width="100%" height="100%"}{: .align-center}

![set](https://user-images.githubusercontent.com/80055816/215414515-420f28e2-a9a4-4be9-a44b-5e24a04963a7.PNG){: width="100%" height="100%"}{: .align-center}

![is](https://user-images.githubusercontent.com/80055816/215414572-f2ebd415-b399-4b25-9e58-7d44bef71817.PNG){: width="100%" height="100%"}{: .align-center}

![backward](https://user-images.githubusercontent.com/80055816/215414642-28c23b67-eab2-4364-b73a-4f10ee12553f.PNG){: width="100%" height="100%"}{: .align-center}

![pose](https://user-images.githubusercontent.com/80055816/215414694-c50c2637-6743-439f-b578-5307827786e8.PNG){: width="100%" height="100%"}{: .align-center}

![last](https://user-images.githubusercontent.com/80055816/215414745-88c790ab-8bd7-40d6-9bb2-ddf3a5eed7f2.PNG){: width="100%" height="100%"}{: .align-center}

![shoot](https://user-images.githubusercontent.com/80055816/215414793-a8c80f35-f3e7-49af-af48-7b9a3121bcdc.PNG){: width="100%" height="100%"}{: .align-center}

<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}