# PHASE | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/

FrameworkPHASECreate dynamic audio experiences in your game or app that react to events and cues in the environment.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+OverviewUse PHASE (Physical Audio Spatialization Engine) to provide complex, dynamic audio experiences in your games and apps. With PHASE, you can control sound layers and adjust audio parameters in real time. As you develop your app, dynamic integration with your app’s visual scene enables audio to react to logic and visual changes automatically. The framework supports various audio hardware, which enables your app to provide a consistent spatial audio experience across platforms and output devices like headphones and speakers.Note If the audio in your game or app doesn’t incorporate environmental events or cues, you can use AVFoundation or Core Audio.Integrate Audio with Visual SimulationApps and games that model a detailed environment involve substantial revision during development. When you provide PHASE with a basic understanding of your app’s scene, audio plays in accordance with the scene’s characteristics. As you modify the scene, such as by adding a game level, the audio follows along by accommodating the level’s visual shape and properties. PHASE couples sound with visuals and minimizes your app’s audio maintenance by:Accepting scene geometry and reducing the volume of obstructed, sound-emitting scene objects. For example, PHASE lowers the volume of an incoming fireball when the player takes cover behind a wall.Offering complex sound events that play in reaction to your app’s runtime state.Adding sound effects that emanate from a shape. When you provide the shape of a scene object to PHASE, the sound’s volume scales based on the player’s distance and orientation relative to the shape.Adding reverberation and timed audio reflection to create environmental effects and simulate indoor scenes.TopicsEssentialsPlaying sound from a location in a 3D scenePosition sound from a specific direction and automatically raise or lower volume based on the environment.Personalizing spatial audio in your appEnhance the realism of spatial audio output by tracking a person’s head movement and accounting for their personal spatial audio profile.PHASE updatesLearn about important changes to PHASE.SetupInitialize an engine object and prepare your app’s audio data for playback.class PHASEEngineAn object that manages audio assets, controls playback, and configures environmental effects.enum UpdateModeModes that determine when the framework consumes API calls and updates internal state.enum RenderingModeModes that determine whether the system renders audio in process or out of process.Betaclass PHASEAssetRegistryA central repository of audio assets.enum PHASENormalizationModeOptions that determine whether the framework adjusts a sound asset’s loudness for the user’s output device.enum PHASESpatializationModeThe manner in which PHASE outputs spatial audio.enum PHASEReverbPresetThe manner in which PHASE diffuses resonating sound.class PHASEMediumA property or quality of the environment that affects how sound travels.Soundscape CreationLay out objects in 3D space to play PHASE audio at runtime that’s consistent with your app’s visual scene.class PHASESourceAn object that plays audio from a 3D location and orientation in a scene.class PHASEListenerA central point of reference that defines the location within the scene that’s most audible to the user.class PHASEOccluderAn object with a shape and position that blocks audio from reaching the listener.class PHASEObjectAn object in the scene.class PHASEShapeA collection of points that connect to form a 3D volume.class ElementAn object that describes the characteristics of a physical surface.class PHASEMaterialSurface characteristics that determine the acoustic properties of an object.enum PHASEMaterialPresetA collection of physical surfaces that each add a unique acoustic quality to your app’s audio.class PHASEMixerParametersAn object that specifies a mixer for sound events and orients them in 3D space.Audio Selection and PlaybackCreate a hierarchy of nodes that tailors playback based on your app’s current state.class PHASESoundAssetA sound resource stored in the asset registry.class PHASESoundEventAn object that determines which audio to play.enum RenderingStateThe playback status of audio.class PHASESoundEventNodeDefinitionA base class for sound event nodes that connect to form a node hierarchy.class PHASESoundEventNodeAssetA template object for sounds that can play in reaction to environmental state.class PHASEAssetA base class that adds a name to framework assets.API ReferenceSound Event NodesObjects that connect to form a hierarchical tree of audio actions.Audio Layering and EffectsChoose among the various ways to play sound depending on your app’s unique audio-playback needs.class PHASEChannelMixerDefinitionAn audio-layering object that routes sound directly to the device’s output.class PHASEAmbientMixerDefinitionAn audio-layering object that outputs sound in a particular direction in 3D space.class PHASEMixerDefinitionAn object to initialize a mixer with a given configuration.class PHASEMixerAn object that combines multiple audio signals into a single signal.class PHASEDefinitionA base class that adds a name to framework definitions.API ReferenceSpatial MixingDefine environmental characteristics that determine how sound plays in your app’s 3D soundscape.Dynamic Sound ControlApply mathematical functions or custom logic to change the properties of in-flight audio or the conditions under which audio plays.class PHASEEnvelopeA collection of segments that connect to graph a complex curve over a linear input.class PHASEEnvelopeSegmentA curved portion of an envelope.enum PHASECurveTypeOptions that apply a mathematical function to an input value.class PHASENumericPairAn ordered pair that defines a bounding box for an envelope.API ReferencePlayback ParameterizationChange the characteristics of in-flight audio by adjusting its properties at runtime.Sound Grouping and ManagementChange the characteristics of a group of sounds, such as altering their volume when your app transitions to a menu.class PHASEGroupA container that shares audio parameters with a collection of sounds.class PHASEGroupPresetA collection of settings for groups.class PHASEGroupPresetSettingSettings for group presets.class PHASEDuckerAn object that manages competing sounds.ErrorsAPI ReferencePHASE ErrorsErrors that the PHASE framework reports.Classesclass PHASEPullStreamNodeclass PHASEPullStreamNodeDefinitionclass PHASEStreamNodeStructuresstruct PHASEAutomaticHeadTrackingFlagsType Aliasestypealias PHASEPullStreamRenderHandler

## Personalizing spatial audio in your app | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/personalizing-spatial-audio-in-your-app

PHASE  Personalizing spatial audio in your app ArticlePersonalizing spatial audio in your appEnhance the realism of spatial audio output by tracking a person’s head movement and accounting for their personal spatial audio profile.iOS 18.0+iPadOS 18.0+macOS 15.0+tvOS 18.0+OverviewApps that implement 3D spatial audio in supported frameworks can fine tune the listener experience by automatically updating the listener orientation according to a person’s head movement while wearing compatible AirPods, and using the personal spatial audio profile that they create in Settings.In iOS 18, iPadOS 18, and tvOS 18, the system adds spatial audio effects for games by default, and offers a Control Center toggle to control the effect. If your game implements custom spatial audio, you need to disable the effect to prevent undesirable artifacts from spatializing an audio stream twice, an effect known as double spatialization.Apply a personal spatial audio profileA person can opt in to personalized spatial audio by creating a profile in settings that walks them through scanning their head using the camera on their iPhone. The system constructs a geometric representation of the shape of the person’s head that supporting audio frameworks observe to enhance the simulation of sound traveling through the physical environment.When you add the com.apple.developer.spatial-audio.profile-access entitlement to your app and implement custom spatial audio with either of the following frameworks, the system automatically takes the personal spatial audio profile into account as it tailors the audio output:AUSpatialMixer Parameters (in Audio Toolbox)AVAudioEnginePHASEEnable head tracking with compatible AirPodsHead tracking adjusts the orientation of the listener according to their head movement while wearing compatible AirPods. This creates the effect that the listener is present in the 3D scene. Head tracking works by simulating the effect of detaching the left and right speakers from the person’s head and virtually placing them in stationary positions in the physical environment, to the left and right of the person, respectively.To enable head tracking:Add the com.apple.developer.coremotion.head-pose entitlement to your app.Configure the API to opt in; the process varies depending on the framework:AVAudioEngineAdjust the AVAudioEnvironmentNode orientation to match the person’s head pose by setting the isListenerHeadTrackingEnabled property to true.PHASEAdjust the PHASEListener orientation by setting the  automaticHeadTrackingFlags property to orientation.Audio ToolboxAdjust the AUSpatialMixer orientation to match the person’s head pose by setting the kAudioUnitProperty_SpatialMixerEnableHeadTracking property to true.Disable the system-provided spatial audioIn iOS 18, iPadOS 18, and tvOS 18, the system adds an automatic spatial audio effect for apps in the App Store Connect game category when a person wears compatible AirPods. If your game already implements spatial audio with one of the supporting frameworks or third-party engine, you need to disable the automatic effect by adding the  AVGameBypassSystemSpatialAudio key to your app’s Info.plist file.Automatic spatial audio works by adding a reverb to the room and simulating the effect of detaching the left and right speakers from the person’s head. The speakers’ output from a virtual position at a fixed length in front of the person, with a short distance between the left and right outputs.Control Center provides UI to toggle this effect and the feature is on by default. If you opt out with the AVGameBypassSystemSpatialAudio key, the system disables the effect and Control Center toggle.See AlsoEssentialsPlaying sound from a location in a 3D scenePosition sound from a specific direction and automatically raise or lower volume based on the environment.PHASE updatesLearn about important changes to PHASE.

## PHASE Errors | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phase-errors

Collection PHASE  PHASE Errors API CollectionPHASE ErrorsErrors that the PHASE framework reports.TopicsFramework Errorsstruct PHASEErrorAn error that PHASE reports.enum CodeCodes that identify errors in PHASE.let PHASEErrorDomain: StringA unique error domain for the framework.Asset Errorsstruct PHASEAssetErrorAn asset error that PHASE reports.enum CodeCodes that identify framework asset errors.let PHASEAssetErrorDomain: StringA unique error domain for PHASE assets.Sound Event Errorsstruct PHASESoundEventErrorA sound event error that PHASE reports.enum CodeCodes that identify sound event errors.let PHASESoundEventErrorDomain: StringA unique error domain for sound events.

## PHASEAmbientMixerDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseambientmixerdefinition

PHASE  PHASEAmbientMixerDefinition ClassPHASEAmbientMixerDefinitionAn audio-layering object that outputs sound in a particular direction in 3D space.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEAmbientMixerDefinitionOverviewAs an audio-layering object, this class combines multiple audio signals to a single signal for the output device. Play audio with a 3D orientation using this class when you supply a quaternion for the orientation argument of the init(channelLayout:orientation:) initializer. For information on orientation the sound, see Working with Quaternions.You also supply the intitializer with a channel layout in either mono, stereo, or surround formats. Surround audio files create the best listening experience due to their extra channel data. The framework renders each channel from the direction of its corresponding speaker in the channel layout. This class ignores low-frequency effect channels that may be present in the layout.Note For one-time sounds that require no position or orientation, use PHASEChannelMixerDefinition instead of this class. If your audio playback needs to react to distance or contain environmental effects, use a spatial mixer; for more information, see Spatial Mixing.Play Sound with a Specific Orientation, Channel Layout, and ListenerTo play ambient sound, define an orientation for the mixer and a channel layout for the source audio data. For example, the following code creates a 5.0 surround-sound ambient source from a 5.1 surround-sound asset.// Orient the mixer.
let orientation: PHASEQuaternion3D = simd_quaternion(1.0, 0.0, 0.0, 0.0)

// Create a channel layout corresponding to the sound asset’s channel layout.
let surroundLayout = AVAudioChannelLayout(
    layoutTag: kAudioChannelLayoutTag_MPEG_5_1_A)

// Create the ambient mixer.
let ambientMixer = PHASEAmbientMixerDefinition(channelLayout: surroundLayout!,
    orientation: orientation)
// Orient the mixer.
PHASEQuaternion3D orientation = simd_quaternion(1.f, 0.f, 0.f, 0.f);

// Create a channel layout corresponding to the sound asset’s channel layout. 
AVAudioChannelLayout* surroundLayout =
    [[AVAudioChannelLayout alloc] initWithLayoutTag:kAudioChannelLayoutTag_MPEG_5_1_A];

// Create the ambient mixer.
PHASEAmbientMixerDefinition* ambientMixer =
    [[PHASEAmbientMixerDefinition alloc] initWithChannelLayout:surroundLayout orientation:orientation];
Ambient mixers require the app to specify a listener, for which you define an orientation by setting the listener’s transform. Continuing on the example above, the following code completes a mixer by attaching a listener, and then plays a sound event.// Attach the mixer to a listener.
let mixerParams = PHASEMixerParameters()
mixerParams.addAmbientMixerParameters(ambientMixer.uid, listener: listener)

// Create a sound event object.    
var ambientSoundEvent: PHASESoundEvent!
do { ambientSoundEvent = try PHASESoundEvent(engine: engine,
        registeredSoundEventNodeAssetUID: ambientSoundEventAsset.uid,
        mixerParameters: mixerParams)
} catch { fatalError("Failed to create a sound event.") }

// Play the ambient sound.
do { try ambientSoundEvent.start() } 
catch { print("Failed to start a sound event.") }
// Attach the mixer to a listener.
PHASEMixerParameters* mixerParams = [[PHASEMixerParameters alloc] init];
[mixerParams addAmbientMixerParameters:ambientMixer.uid
    listener:_listener];

// Create a sound event object.    
PHASESoundEvent* ambientSoundEvent =
    [[PHASESoundEvent alloc]initWithEngine:_engine
        registeredSoundEventNodeAssetUID:ambientSoundEventAsset.uid
        mixerParameters:mixerParams
        outError:&err];

// Play the ambient sound.
[ambientSoundEvent startAndReturnError:&err];
PHASE changes the channel output of ambient-mixer sound dynamically, depending on the respective directions of the mixer and the listener. For example, you can use an ambient mixer in a game to play the environmental sound of birds all around and the sound of traffic on a road in just one audio channel. Depending on the direction the player is facing, the mixer can rotate the audio so that the road always sounds like it’s coming from the same direction, for example, the west.TopicsCreating an Ambient Mixerinit(channelLayout: AVAudioChannelLayout, orientation: simd_quatf)Creates an ambient mixer with the given channel layout and orientation.convenience init(channelLayout: AVAudioChannelLayout, orientation: simd_quatf, identifier: String)Creates a named ambient mixer with the given channel layout and orientation.Inspecting the Mixervar inputChannelLayout: AVAudioChannelLayoutThe channel layout of input audio.var orientation: simd_quatfA quaternion that describes the orientation of the speaker layout relative to the scene origin.RelationshipsInherits FromPHASEMixerDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoAudio Layering and Effectsclass PHASEChannelMixerDefinitionAn audio-layering object that routes sound directly to the device’s output.class PHASEMixerDefinitionAn object to initialize a mixer with a given configuration.class PHASEMixerAn object that combines multiple audio signals into a single signal.class PHASEDefinitionA base class that adds a name to framework definitions.API ReferenceSpatial MixingDefine environmental characteristics that determine how sound plays in your app’s 3D soundscape.

### init(channelLayout:orientation:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseambientmixerdefinition/init(channellayout:orientation:)

PHASE  PHASEAmbientMixerDefinition  init(channelLayout:orientation:) Initializerinit(channelLayout:orientation:)Creates an ambient mixer with the given channel layout and orientation.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    channelLayout layout: AVAudioChannelLayout,
    orientation: simd_quatf
) Parameters layoutThe channel layout of input audio.orientationA quaternion that describes the orientation of the speaker layout relative to the scene origin.See AlsoCreating an Ambient Mixerconvenience init(channelLayout: AVAudioChannelLayout, orientation: simd_quatf, identifier: String)Creates a named ambient mixer with the given channel layout and orientation.

### init(channelLayout:orientation:identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseambientmixerdefinition/init(channellayout:orientation:identifier:)

PHASE  PHASEAmbientMixerDefinition  init(channelLayout:orientation:identifier:) Initializerinit(channelLayout:orientation:identifier:)Creates a named ambient mixer with the given channel layout and orientation.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+convenience init(
    channelLayout layout: AVAudioChannelLayout,
    orientation: simd_quatf,
    identifier: String
) Parameters layoutThe channel layout of input audio.orientationA quaternion that describes the orientation of the speaker layout relative to the scene origin.identifierA unique name for the mixer.See AlsoCreating an Ambient Mixerinit(channelLayout: AVAudioChannelLayout, orientation: simd_quatf)Creates an ambient mixer with the given channel layout and orientation.

### inputChannelLayout | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseambientmixerdefinition/inputchannellayout

PHASE  PHASEAmbientMixerDefinition  inputChannelLayout Instance PropertyinputChannelLayoutThe channel layout of input audio.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var inputChannelLayout: AVAudioChannelLayout { get }DiscussionThe framework sets the value to the channelLayout initializer argument. See init(channelLayout:orientation:).See AlsoInspecting the Mixervar orientation: simd_quatfA quaternion that describes the orientation of the speaker layout relative to the scene origin.

### orientation | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseambientmixerdefinition/orientation

PHASE  PHASEAmbientMixerDefinition  orientation Instance PropertyorientationA quaternion that describes the orientation of the speaker layout relative to the scene origin.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var orientation: simd_quatf { get }DiscussionThe framework sets the value to the orientation initializer argument. See init(channelLayout:orientation:).See AlsoInspecting the Mixervar inputChannelLayout: AVAudioChannelLayoutThe channel layout of input audio.

## PHASEAsset | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasset

PHASE  PHASEAsset ClassPHASEAssetA base class that adds a name to framework assets.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEAssetOverviewThrough inheritance, this class adds a string identifier to subclasses, for example, PHASESoundAsset and PHASESoundEventNodeAsset.PHASE generates objects of this type based on template PHASEDefinition subclasses. For example, PHASE gives you a PHASESoundEventNodeAsset when you register a PHASESoundEventNodeDefinition with the asset registry via registerSoundEventAsset(rootNode:identifier:).TopicsIdentifying an Assetvar identifier: StringA unique name for the asset.Classifying an Assetenum AssetTypeOptions that determine how PHASE manages sound assets in memory.RelationshipsInherits FromNSObjectInherited ByPHASEGlobalMetaParameterAssetPHASESoundAssetPHASESoundEventNodeAssetConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoAudio Selection and Playbackclass PHASESoundAssetA sound resource stored in the asset registry.class PHASESoundEventAn object that determines which audio to play.enum RenderingStateThe playback status of audio.class PHASESoundEventNodeDefinitionA base class for sound event nodes that connect to form a node hierarchy.class PHASESoundEventNodeAssetA template object for sounds that can play in reaction to environmental state.API ReferenceSound Event NodesObjects that connect to form a hierarchical tree of audio actions.

### PHASEAsset.AssetType | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasset/assettype

PHASE  PHASEAsset  PHASEAsset.AssetType EnumerationPHASEAsset.AssetTypeOptions that determine how PHASE manages sound assets in memory.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum AssetTypeOverviewTo prepare for playback, the framework can decompress a sound asset or perform a format conversion, or both, depending on the type of the underlying asset data.TopicsTypescase residentA sound asset that plays after fully loading in memory.case streamedA sound asset that streams from disk into memory as it plays.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatype

#### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasset/assettype/init(rawvalue:)

PHASE  PHASEAsset  PHASEAsset  PHASEAsset.AssetType  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

#### PHASEAsset.AssetType.resident | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasset/assettype/resident

PHASE  PHASEAsset  PHASEAsset  PHASEAsset.AssetType  PHASEAsset.AssetType.resident CasePHASEAsset.AssetType.residentA sound asset that plays after fully loading in memory.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case residentDiscussionIf the sound asset is in memory, the framework prepares it for playback. If the asset is on disk, the framework loads it into memory, and prepares it for playback.See AlsoTypescase streamedA sound asset that streams from disk into memory as it plays.

#### PHASEAsset.AssetType.streamed | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasset/assettype/streamed

PHASE  PHASEAsset  PHASEAsset  PHASEAsset.AssetType  PHASEAsset.AssetType.streamed CasePHASEAsset.AssetType.streamedA sound asset that streams from disk into memory as it plays.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case streamedDiscussionIf the asset is on disk, the framework streams the asset’s data from disk into memory and prepares the asset during playback. If the asset is in memory, the framework streams from memory and prepares the asset during playback.See AlsoTypescase residentA sound asset that plays after fully loading in memory.

### identifier | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasset/identifier

PHASE  PHASEAsset  identifier Instance PropertyidentifierA unique name for the asset.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var identifier: String { get }

## PHASEAssetError | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterror-swift.struct

PHASE  PHASEAssetError StructurePHASEAssetErrorAn asset error that PHASE reports.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+struct PHASEAssetErrorTopicsCreating an Errorenum CodeCodes that identify framework asset errors.Identifying an Error Causestatic var alreadyExists: PHASEAssetError.CodeAn error the asset registry throws when the app registers an asset twice by the same name.static var badParameters: PHASEAssetError.CodeAn error that indicates an asset registry call contains invalid data.static var failedToLoad: PHASEAssetError.CodeAn error that indicates an asset failed to load.static var generalError: PHASEAssetError.CodeAn error the asset registry throws when an unspecified problem occurs.static var invalidEngineInstance: PHASEAssetError.CodeAn error that indicates an asset registry call references an invalid engine.static var memoryAllocation: PHASEAssetError.CodeAn error the framework throws when an asset depletes system memory.Type Propertiesstatic var errorDomain: StringRelationshipsConforms ToCustomNSErrorEquatableErrorHashableSendableSendableMetatypeSee AlsoAsset Errorsenum CodeCodes that identify framework asset errors.let PHASEAssetErrorDomain: StringA unique error domain for PHASE assets.

### alreadyExists | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterror-swift.struct/alreadyexists

PHASE  PHASEAssetError  alreadyExists Type PropertyalreadyExistsAn error the asset registry throws when the app registers an asset twice by the same name.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var alreadyExists: PHASEAssetError.Code { get }See AlsoIdentifying an Error Causestatic var badParameters: PHASEAssetError.CodeAn error that indicates an asset registry call contains invalid data.static var failedToLoad: PHASEAssetError.CodeAn error that indicates an asset failed to load.static var generalError: PHASEAssetError.CodeAn error the asset registry throws when an unspecified problem occurs.static var invalidEngineInstance: PHASEAssetError.CodeAn error that indicates an asset registry call references an invalid engine.static var memoryAllocation: PHASEAssetError.CodeAn error the framework throws when an asset depletes system memory.

### badParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterror-swift.struct/badparameters

PHASE  PHASEAssetError  badParameters Type PropertybadParametersAn error that indicates an asset registry call contains invalid data.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var badParameters: PHASEAssetError.Code { get }See AlsoIdentifying an Error Causestatic var alreadyExists: PHASEAssetError.CodeAn error the asset registry throws when the app registers an asset twice by the same name.static var failedToLoad: PHASEAssetError.CodeAn error that indicates an asset failed to load.static var generalError: PHASEAssetError.CodeAn error the asset registry throws when an unspecified problem occurs.static var invalidEngineInstance: PHASEAssetError.CodeAn error that indicates an asset registry call references an invalid engine.static var memoryAllocation: PHASEAssetError.CodeAn error the framework throws when an asset depletes system memory.

### PHASEAssetError.Code | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterror-swift.struct/code

PHASE  PHASEAssetError  PHASEAssetError.Code EnumerationPHASEAssetError.CodeCodes that identify framework asset errors.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum CodeTopicsErrorscase alreadyExistsAn error the asset registry throws when the app registers an asset twice by the same name.case badParametersAn error that indicates an asset registry call contains invalid data.case failedToLoadAn error that indicates an asset failed to load.case generalErrorAn error the asset registry throws when an unspecified problem occurs.case invalidEngineInstanceAn error that indicates an asset registry call references an invalid engine.case memoryAllocationAn error the framework throws when an asset depletes system memory.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoAsset Errorsstruct PHASEAssetErrorAn asset error that PHASE reports.let PHASEAssetErrorDomain: StringA unique error domain for PHASE assets.

#### PHASEAssetError.Code.alreadyExists | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterror-swift.struct/code/alreadyexists

PHASE  PHASEAssetError  PHASEAssetError  PHASEAssetError.Code  PHASEAssetError.Code.alreadyExists CasePHASEAssetError.Code.alreadyExistsAn error the asset registry throws when the app registers an asset twice by the same name.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case alreadyExistsSee AlsoErrorscase badParametersAn error that indicates an asset registry call contains invalid data.case failedToLoadAn error that indicates an asset failed to load.case generalErrorAn error the asset registry throws when an unspecified problem occurs.case invalidEngineInstanceAn error that indicates an asset registry call references an invalid engine.case memoryAllocationAn error the framework throws when an asset depletes system memory.

#### PHASEAssetError.Code.badParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterror-swift.struct/code/badparameters

PHASE  PHASEAssetError  PHASEAssetError  PHASEAssetError.Code  PHASEAssetError.Code.badParameters CasePHASEAssetError.Code.badParametersAn error that indicates an asset registry call contains invalid data.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case badParametersSee AlsoErrorscase alreadyExistsAn error the asset registry throws when the app registers an asset twice by the same name.case failedToLoadAn error that indicates an asset failed to load.case generalErrorAn error the asset registry throws when an unspecified problem occurs.case invalidEngineInstanceAn error that indicates an asset registry call references an invalid engine.case memoryAllocationAn error the framework throws when an asset depletes system memory.

#### PHASEAssetError.Code.failedToLoad | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterror-swift.struct/code/failedtoload

PHASE  PHASEAssetError  PHASEAssetError  PHASEAssetError.Code  PHASEAssetError.Code.failedToLoad CasePHASEAssetError.Code.failedToLoadAn error that indicates an asset failed to load.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case failedToLoadSee AlsoErrorscase alreadyExistsAn error the asset registry throws when the app registers an asset twice by the same name.case badParametersAn error that indicates an asset registry call contains invalid data.case generalErrorAn error the asset registry throws when an unspecified problem occurs.case invalidEngineInstanceAn error that indicates an asset registry call references an invalid engine.case memoryAllocationAn error the framework throws when an asset depletes system memory.

#### PHASEAssetError.Code.generalError | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterror-swift.struct/code/generalerror

PHASE  PHASEAssetError  PHASEAssetError  PHASEAssetError.Code  PHASEAssetError.Code.generalError CasePHASEAssetError.Code.generalErrorAn error the asset registry throws when an unspecified problem occurs.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case generalErrorSee AlsoErrorscase alreadyExistsAn error the asset registry throws when the app registers an asset twice by the same name.case badParametersAn error that indicates an asset registry call contains invalid data.case failedToLoadAn error that indicates an asset failed to load.case invalidEngineInstanceAn error that indicates an asset registry call references an invalid engine.case memoryAllocationAn error the framework throws when an asset depletes system memory.

#### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterror-swift.struct/code/init(rawvalue:)

PHASE  PHASEAssetError  PHASEAssetError  PHASEAssetError.Code  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

#### PHASEAssetError.Code.invalidEngineInstance | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterror-swift.struct/code/invalidengineinstance

PHASE  PHASEAssetError  PHASEAssetError  PHASEAssetError.Code  PHASEAssetError.Code.invalidEngineInstance CasePHASEAssetError.Code.invalidEngineInstanceAn error that indicates an asset registry call references an invalid engine.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case invalidEngineInstanceSee AlsoErrorscase alreadyExistsAn error the asset registry throws when the app registers an asset twice by the same name.case badParametersAn error that indicates an asset registry call contains invalid data.case failedToLoadAn error that indicates an asset failed to load.case generalErrorAn error the asset registry throws when an unspecified problem occurs.case memoryAllocationAn error the framework throws when an asset depletes system memory.

#### PHASEAssetError.Code.memoryAllocation | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterror-swift.struct/code/memoryallocation

PHASE  PHASEAssetError  PHASEAssetError  PHASEAssetError.Code  PHASEAssetError.Code.memoryAllocation CasePHASEAssetError.Code.memoryAllocationAn error the framework throws when an asset depletes system memory.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case memoryAllocationSee AlsoErrorscase alreadyExistsAn error the asset registry throws when the app registers an asset twice by the same name.case badParametersAn error that indicates an asset registry call contains invalid data.case failedToLoadAn error that indicates an asset failed to load.case generalErrorAn error the asset registry throws when an unspecified problem occurs.case invalidEngineInstanceAn error that indicates an asset registry call references an invalid engine.

### errorDomain | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterror-swift.struct/errordomain

PHASE  PHASEAssetError  errorDomain Type PropertyerrorDomainiOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var errorDomain: String { get }

### failedToLoad | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterror-swift.struct/failedtoload

PHASE  PHASEAssetError  failedToLoad Type PropertyfailedToLoadAn error that indicates an asset failed to load.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var failedToLoad: PHASEAssetError.Code { get }See AlsoIdentifying an Error Causestatic var alreadyExists: PHASEAssetError.CodeAn error the asset registry throws when the app registers an asset twice by the same name.static var badParameters: PHASEAssetError.CodeAn error that indicates an asset registry call contains invalid data.static var generalError: PHASEAssetError.CodeAn error the asset registry throws when an unspecified problem occurs.static var invalidEngineInstance: PHASEAssetError.CodeAn error that indicates an asset registry call references an invalid engine.static var memoryAllocation: PHASEAssetError.CodeAn error the framework throws when an asset depletes system memory.

### generalError | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterror-swift.struct/generalerror

PHASE  PHASEAssetError  generalError Type PropertygeneralErrorAn error the asset registry throws when an unspecified problem occurs.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var generalError: PHASEAssetError.Code { get }See AlsoIdentifying an Error Causestatic var alreadyExists: PHASEAssetError.CodeAn error the asset registry throws when the app registers an asset twice by the same name.static var badParameters: PHASEAssetError.CodeAn error that indicates an asset registry call contains invalid data.static var failedToLoad: PHASEAssetError.CodeAn error that indicates an asset failed to load.static var invalidEngineInstance: PHASEAssetError.CodeAn error that indicates an asset registry call references an invalid engine.static var memoryAllocation: PHASEAssetError.CodeAn error the framework throws when an asset depletes system memory.

### invalidEngineInstance | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterror-swift.struct/invalidengineinstance

PHASE  PHASEAssetError  invalidEngineInstance Type PropertyinvalidEngineInstanceAn error that indicates an asset registry call references an invalid engine.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var invalidEngineInstance: PHASEAssetError.Code { get }See AlsoIdentifying an Error Causestatic var alreadyExists: PHASEAssetError.CodeAn error the asset registry throws when the app registers an asset twice by the same name.static var badParameters: PHASEAssetError.CodeAn error that indicates an asset registry call contains invalid data.static var failedToLoad: PHASEAssetError.CodeAn error that indicates an asset failed to load.static var generalError: PHASEAssetError.CodeAn error the asset registry throws when an unspecified problem occurs.static var memoryAllocation: PHASEAssetError.CodeAn error the framework throws when an asset depletes system memory.

### memoryAllocation | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterror-swift.struct/memoryallocation

PHASE  PHASEAssetError  memoryAllocation Type PropertymemoryAllocationAn error the framework throws when an asset depletes system memory.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var memoryAllocation: PHASEAssetError.Code { get }See AlsoIdentifying an Error Causestatic var alreadyExists: PHASEAssetError.CodeAn error the asset registry throws when the app registers an asset twice by the same name.static var badParameters: PHASEAssetError.CodeAn error that indicates an asset registry call contains invalid data.static var failedToLoad: PHASEAssetError.CodeAn error that indicates an asset failed to load.static var generalError: PHASEAssetError.CodeAn error the asset registry throws when an unspecified problem occurs.static var invalidEngineInstance: PHASEAssetError.CodeAn error that indicates an asset registry call references an invalid engine.

## PHASEAssetErrorDomain | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseasseterrordomain

PHASE  PHASEAssetErrorDomain Global VariablePHASEAssetErrorDomainA unique error domain for PHASE assets.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+let PHASEAssetErrorDomain: StringDiscussionFor more information on Core Foundation error domains, see Error domains.See AlsoAsset Errorsstruct PHASEAssetErrorAn asset error that PHASE reports.enum CodeCodes that identify framework asset errors.

## PHASEAssetRegistry | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseassetregistry

PHASE  PHASEAssetRegistry ClassPHASEAssetRegistryA central repository of audio assets.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEAssetRegistryOverviewThis class manages audio by registering two types of assets throughout the app’s life cycle:PHASESoundAssetA sound asset identifies the particular audio data that your app intends to play.PHASESoundEventNodeAssetA sound event asset provides audio with an avenue to the output device, and either represents a single sound or a dynamic set of sounds that play individually, depending on the app’s state.When you’re done with a sound asset, call unregisterAsset(identifier:completion:) to free up its system resources.TopicsRegistering Sound AssetsLoad shared audio data that your app can access and play from any scope.func registerSoundAsset(url: URL, identifier: String?, assetType: PHASEAsset.AssetType, channelLayout: AVAudioChannelLayout?, normalizationMode: PHASENormalizationMode) throws -> PHASESoundAssetLoads a sound asset from the argument URL and adds it to the engine’s list of registered assets.func registerSoundAsset(data: Data, identifier: String?, format: AVAudioFormat, normalizationMode: PHASENormalizationMode) throws -> PHASESoundAssetLoads a sound asset from memory and adds it to the engine’s list of registered assets.func unregisterAsset(identifier: String, completion: ((Bool) -> Void)?)Deallocates system memory for a given asset and removes it from the engine’s list of registered assets.Registering Sound Event AssetsDefine playback objects that your app invokes for one-time audio output, or a sophisticated hierarchy that varies the output based on your app’s state.func registerSoundEventAsset(rootNode: PHASESoundEventNodeDefinition, identifier: String?) throws -> PHASESoundEventNodeAssetRegisters the root node of the sound event asset.func asset(forIdentifier: String) -> PHASEAsset?Provides the asset named with the designated identifier.Registering Global MetaparametersCentralize audio parameters that change the charactaristics of in-flight audio, and synchronize across multiple playback events.func registerGlobalMetaParameter(metaParameterDefinition: PHASEMetaParameterDefinition) throws -> PHASEGlobalMetaParameterAssetRegisters a global metaparameter with the asset registry.var globalMetaParameters: [String : PHASEMetaParameter]A dictionary of metaparameters that all sound event assets share.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSetupclass PHASEEngineAn object that manages audio assets, controls playback, and configures environmental effects.enum UpdateModeModes that determine when the framework consumes API calls and updates internal state.enum RenderingModeModes that determine whether the system renders audio in process or out of process.Betaenum PHASENormalizationModeOptions that determine whether the framework adjusts a sound asset’s loudness for the user’s output device.enum PHASESpatializationModeThe manner in which PHASE outputs spatial audio.enum PHASEReverbPresetThe manner in which PHASE diffuses resonating sound.class PHASEMediumA property or quality of the environment that affects how sound travels.

### asset(forIdentifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseassetregistry/asset(foridentifier:)

PHASE  PHASEAssetRegistry  asset(forIdentifier:) Instance Methodasset(forIdentifier:)Provides the asset named with the designated identifier.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func asset(forIdentifier identifier: String) -> PHASEAsset? Parameters identifierThe unique name of the asset.Return ValueA framework asset by the destignated name, if the app registers the asset prior. Otherwise, returns nil.See AlsoRegistering Sound Event Assetsfunc registerSoundEventAsset(rootNode: PHASESoundEventNodeDefinition, identifier: String?) throws -> PHASESoundEventNodeAssetRegisters the root node of the sound event asset.

### globalMetaParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseassetregistry/globalmetaparameters

PHASE  PHASEAssetRegistry  globalMetaParameters Instance PropertyglobalMetaParametersA dictionary of metaparameters that all sound event assets share.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var globalMetaParameters: [String : PHASEMetaParameter] { get }DiscussionWhen you change a value for a metaparameter in this dictionary, every sound event attached to the metaparameter observes the change. The dictionary key is the identifier of the PHASEMetaParameterDefinition you pass into registerGlobalMetaParameter(metaParameterDefinition:).Tip To adjust a value for a single sound event, access the metaparameter through the metaParameters property instead.See AlsoRegistering Global Metaparametersfunc registerGlobalMetaParameter(metaParameterDefinition: PHASEMetaParameterDefinition) throws -> PHASEGlobalMetaParameterAssetRegisters a global metaparameter with the asset registry.

### registerGlobalMetaParameter(metaParameterDefinition:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseassetregistry/registerglobalmetaparameter(metaparameterdefinition:)

PHASE  PHASEAssetRegistry  registerGlobalMetaParameter(metaParameterDefinition:) Instance MethodregisterGlobalMetaParameter(metaParameterDefinition:)Registers a global metaparameter with the asset registry.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func registerGlobalMetaParameter(metaParameterDefinition: PHASEMetaParameterDefinition) throws -> PHASEGlobalMetaParameterAsset Parameters metaParameterDefinitionA single parameter that controls the value of multiple parameters.Return ValueA global metaparameter object. If an error occurs, the function returns nil.DiscussionGlobal metaparameters attach to any number of sound event assets. When an app adjusts a global metaparameter at runtime, the change propagates immediately to all the attached sound events.Note Although you register a global metaparameter definition (PHASEMetaParameterDefinition) with this function, you receive a global metaparameter instance (PHASEMetaParameter) when you access the parameter by its identifier using the globalMetaParameters dictionary.See AlsoRegistering Global Metaparametersvar globalMetaParameters: [String : PHASEMetaParameter]A dictionary of metaparameters that all sound event assets share.

### registerSoundAsset(data:identifier:format:normalizationMode:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseassetregistry/registersoundasset(data:identifier:format:normalizationmode:)

PHASE  PHASEAssetRegistry  registerSoundAsset(data:identifier:format:normalizationMode:) Instance MethodregisterSoundAsset(data:identifier:format:normalizationMode:)Loads a sound asset from memory and adds it to the engine’s list of registered assets.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func registerSoundAsset(
    data: Data,
    identifier: String?,
    format: AVAudioFormat,
    normalizationMode: PHASENormalizationMode
) throws -> PHASESoundAsset Parameters dataA buffer containing the audio data to register. Audio data needs to be single-channel interleaved PCM, or per-channel de-interleaved PCM with buffers organized back to back.identifierA unique name for the sound asset. If you provide nil, the framework determines and sets value for the asset’s identifier.formatAnd object that describes the audio data layout.normalizationModeAn option to calibrate the sound asset for the user’s output device.Return ValueA sound asset object. If an error occurs, the function returns nil.See AlsoRegistering Sound Assetsfunc registerSoundAsset(url: URL, identifier: String?, assetType: PHASEAsset.AssetType, channelLayout: AVAudioChannelLayout?, normalizationMode: PHASENormalizationMode) throws -> PHASESoundAssetLoads a sound asset from the argument URL and adds it to the engine’s list of registered assets.func unregisterAsset(identifier: String, completion: ((Bool) -> Void)?)Deallocates system memory for a given asset and removes it from the engine’s list of registered assets.

### registerSoundAsset(url:identifier:assetType:channelLayout:normalizationMode:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseassetregistry/registersoundasset(url:identifier:assettype:channellayout:normalizationmode:)

PHASE  PHASEAssetRegistry  registerSoundAsset(url:identifier:assetType:channelLayout:normalizationMode:) Instance MethodregisterSoundAsset(url:identifier:assetType:channelLayout:normalizationMode:)Loads a sound asset from the argument URL and adds it to the engine’s list of registered assets.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func registerSoundAsset(
    url: URL,
    identifier: String?,
    assetType: PHASEAsset.AssetType,
    channelLayout: AVAudioChannelLayout?,
    normalizationMode: PHASENormalizationMode
) throws -> PHASESoundAsset Parameters urlA URL to an audio file on disk. This function doesn’t support network URLs.identifierA unique name for the sound asset. If you provide nil, the framework determines and sets value for the asset’s identifier.assetTypeThe asset’s type.channelLayoutAn object that describes an audio channel layout to replace the asset’s channel layout. This channel layout needs to have the same channel count as the asset or this function returns an error. Some multichannel files—that is, files with more than two channels—don’t contain a channel layout. WAV files may not contain a channel layout, whereas CAF files normally do. This function checks if a channel layout exists in a file and if so, PHASE uses it.If the asset is stereo or mono, you can pass nil because the framework generates the channel layout for you in that case.normalizationModeAn option to calibrate the sound asset for the user’s output device.Return ValueA sound asset object. If an error occurs, the function returns nil.DiscussionTo expedite audio loading, run this function for multiple assets on multiple threads. This function runs synchronously. As a thread-safe function, you can run it off the main thread.See AlsoRegistering Sound Assetsfunc registerSoundAsset(data: Data, identifier: String?, format: AVAudioFormat, normalizationMode: PHASENormalizationMode) throws -> PHASESoundAssetLoads a sound asset from memory and adds it to the engine’s list of registered assets.func unregisterAsset(identifier: String, completion: ((Bool) -> Void)?)Deallocates system memory for a given asset and removes it from the engine’s list of registered assets.

### registerSoundEventAsset(rootNode:identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseassetregistry/registersoundeventasset(rootnode:identifier:)

PHASE  PHASEAssetRegistry  registerSoundEventAsset(rootNode:identifier:) Instance MethodregisterSoundEventAsset(rootNode:identifier:)Registers the root node of the sound event asset.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func registerSoundEventAsset(
    rootNode: PHASESoundEventNodeDefinition,
    identifier: String?
) throws -> PHASESoundEventNodeAsset Parameters rootNodeThe root node of the sound event asset to register.identifierThe identifier to assign to this parameter. Assigning nil generates an automatic identifier.Return ValueA sound event node asset.See AlsoRegistering Sound Event Assetsfunc asset(forIdentifier: String) -> PHASEAsset?Provides the asset named with the designated identifier.

### unregisterAsset(identifier:completion:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseassetregistry/unregisterasset(identifier:completion:)

PHASE  PHASEAssetRegistry  unregisterAsset(identifier:completion:) Instance MethodunregisterAsset(identifier:completion:)Deallocates system memory for a given asset and removes it from the engine’s list of registered assets.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func unregisterAsset(
    identifier: String,
    completion handler: ((Bool) -> Void)? = nil
)func unregisterAsset(identifier: String) async -> Bool Parameters identifierThe unique name that the app defines for the sound asset.handlerCode that the system runs after it unregisters the asset.DiscussionImportant You can call this method from synchronous code using a completion handler, as shown on this page, or you can call it as an asynchronous method that has the following declaration:func unregisterAsset(identifier: String) async -> Bool
For information about concurrency and asynchronous code in Swift, see Calling Objective-C APIs Asynchronously.See AlsoRegistering Sound Assetsfunc registerSoundAsset(url: URL, identifier: String?, assetType: PHASEAsset.AssetType, channelLayout: AVAudioChannelLayout?, normalizationMode: PHASENormalizationMode) throws -> PHASESoundAssetLoads a sound asset from the argument URL and adds it to the engine’s list of registered assets.func registerSoundAsset(data: Data, identifier: String?, format: AVAudioFormat, normalizationMode: PHASENormalizationMode) throws -> PHASESoundAssetLoads a sound asset from memory and adds it to the engine’s list of registered assets.

## PHASEAutomaticHeadTrackingFlags | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseautomaticheadtrackingflags

PHASE  PHASEAutomaticHeadTrackingFlags StructurePHASEAutomaticHeadTrackingFlagsiOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 26.0+Betastruct PHASEAutomaticHeadTrackingFlagsOverviewAutomatic Head-Tracking flags.On capable devices, listener orientation will be automatically rotated based on user's head-orientation.
On capable devices, listener position will be automatically set based on user's position.
TopicsInitializersinit(rawValue: UInt)Type Propertiesstatic var orientation: PHASEAutomaticHeadTrackingFlagsstatic var position: PHASEAutomaticHeadTrackingFlagsRelationshipsConforms ToBitwiseCopyableEquatableExpressibleByArrayLiteralOptionSetRawRepresentableSendableSendableMetatypeSetAlgebraBeta Software This documentation contains preliminary information about an API or technology in development. This information is subject to change, and software implemented according to this documentation should be tested with final operating system software.  Learn more about using Apple's beta software

### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseautomaticheadtrackingflags/init(rawvalue:)

PHASE  PHASEAutomaticHeadTrackingFlags  init(rawValue:) Initializerinit(rawValue:)iOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 26.0+Betainit(rawValue: UInt)Beta Software This documentation contains preliminary information about an API or technology in development. This information is subject to change, and software implemented according to this documentation should be tested with final operating system software.  Learn more about using Apple's beta software

### orientation | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseautomaticheadtrackingflags/orientation

PHASE  PHASEAutomaticHeadTrackingFlags  orientation Type PropertyorientationiOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 26.0+Betastatic var orientation: PHASEAutomaticHeadTrackingFlags { get }Beta Software This documentation contains preliminary information about an API or technology in development. This information is subject to change, and software implemented according to this documentation should be tested with final operating system software.  Learn more about using Apple's beta software

### position | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseautomaticheadtrackingflags/position

PHASE  PHASEAutomaticHeadTrackingFlags  position Type PropertypositioniOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 26.0+Betastatic var position: PHASEAutomaticHeadTrackingFlags { get }Beta Software This documentation contains preliminary information about an API or technology in development. This information is subject to change, and software implemented according to this documentation should be tested with final operating system software.  Learn more about using Apple's beta software

## PHASEBlendNodeDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseblendnodedefinition

PHASE  PHASEBlendNodeDefinition ClassPHASEBlendNodeDefinitionA node that smoothly fades between the audio of its child nodes.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEBlendNodeDefinitionOverviewThis class defines a threshold and a numeric parameter the app increases and decreases to fade between child nodes. Each child node defines a range within the threshold in which the child node plays audio. As the app moves the blend parameter value between 0 and the threshold, the blend node plays the audio of its child nodes whose range and fade curve overlap at the current value.Play a Blend of Simultaneous Audio DataTo gradually change the audio that a sound event plays, define blend thresholds and a number metaparameter that incrementally increases or decreases between the thresholds. For example, the following code sets up a sound event hierarchy containing two sampler nodes that play audio, with each one modeling a different terrain. The app sets the metaparameter value based on the value of the terrain the player stands on. When the app starts a sound event from this hierarchy, PHASE plays:A grass footstep for terrain values between 0 and 0.33A cobblestone footstep for terrain values between 0.67 and 1.0A blend of both footstep sounds for values between 0.33 and 0.67// Create a meta parameter definition that chooses among different terrains.
let terrainBlendParameter = PHASENumberMetaParameterDefinition(
    value: 0.5, 
    minimum: 0.0,
    maximum: 1.0,
    identifier: "terrain")

// Create a blend node and pass in the meta parameter.
let terrainBlendNode = PHASEBlendNodeDefinition(blendMetaParameterDefinition: terrainBlendParameter)

// Add two samples nodes to blend between.
terrainBlendNode.addRangeForInputValuesAbove( 
    value: 0.33,
    fullGainAtValue: 1.0,
    fadeCurveType: .linear,
    subtree:cobblestoneSamplerNode)

terrainBlendNode.addRangeForInputValuesBelow( 
    value: 0.67,
    fullGainAtValue: 0.0,
    fadeCurveType: .linear,
    subtree:grassSamplerNode)

// Create a sound event.
var footstepEvent: PHASESoundEvent?
do { footstepEvent = try PHASESoundEvent(engine: myEngine, assetIdentifier: "terrain") } 
catch { fatalError("Failed to create the sound event due to: \(error)") }        

// Set the "terrain" metaparameter value to a midpoint that 
//  plays audio from both subtrees at an equal volume.
guard let terrainParameter = footstepEvent?.metaParameters["terrain"] else { fatalError() }
terrainParameter.value = 0.5

// Play the sound and hear a mix of both terrains.
footstepEvent?.start() { reason in 
/* Perform completion tasks. */ }
TopicsCreating a Blend Nodeinit(blendMetaParameterDefinition: PHASENumberMetaParameterDefinition)Creates a blend node with a maxiumum blend range value.convenience init(blendMetaParameterDefinition: PHASENumberMetaParameterDefinition, identifier: String)Creates a named blend node with a maxiumum blend range value.init(spatialMixerDefinition: PHASESpatialMixerDefinition)Creates a blend node for spatial audio output.convenience init(spatialMixerDefinition: PHASESpatialMixerDefinition, identifier: String)Creates a named blend node for spatial audio output.Accessing Blend Propertiesvar blendParameterDefinition: PHASENumberMetaParameterDefinition?The meta parameter definition that caps the blend range.var spatialMixerDefinitionForDistance: PHASESpatialMixerDefinition?An object that combines spatial audio layers.Adding Child Nodesfunc addRange(envelope: PHASEEnvelope, subtree: PHASESoundEventNodeDefinition)Adds a child node with an envelope.func addRangeForInputValuesAbove(value: Double, fullGainAtValue: Double, fadeCurveType: PHASECurveType, subtree: PHASESoundEventNodeDefinition)Adds a child node that blends above a given value.func addRangeForInputValuesBelow(value: Double, fullGainAtValue: Double, fadeCurveType: PHASECurveType, subtree: PHASESoundEventNodeDefinition)Adds a child node that blends below a given value.func addRangeForInputValuesBetween(lowValue: Double, highValue: Double, fullGainAtLowValue: Double, fullGainAtHighValue: Double, lowFadeCurveType: PHASECurveType, highFadeCurveType: PHASECurveType, subtree: PHASESoundEventNodeDefinition)Adds a child node that blends between a given high and low value.RelationshipsInherits FromPHASESoundEventNodeDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoControl Nodesclass PHASESwitchNodeDefinitionA node that passes invocation to only one of its child nodes.class PHASERandomNodeDefinitionA sound event node that invokes one of its child nodes at random.class PHASEContainerNodeDefinitionA node that plays all its children at the same time.

### addRange(envelope:subtree:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseblendnodedefinition/addrange(envelope:subtree:)

PHASE  PHASEBlendNodeDefinition  addRange(envelope:subtree:) Instance MethodaddRange(envelope:subtree:)Adds a child node with an envelope.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func addRange(
    envelope: PHASEEnvelope,
    subtree: PHASESoundEventNodeDefinition
) Parameters envelopeA shaped audio signal over a range.subtreeA child node that’s active in the blend range an envelope defines.See AlsoAdding Child Nodesfunc addRangeForInputValuesAbove(value: Double, fullGainAtValue: Double, fadeCurveType: PHASECurveType, subtree: PHASESoundEventNodeDefinition)Adds a child node that blends above a given value.func addRangeForInputValuesBelow(value: Double, fullGainAtValue: Double, fadeCurveType: PHASECurveType, subtree: PHASESoundEventNodeDefinition)Adds a child node that blends below a given value.func addRangeForInputValuesBetween(lowValue: Double, highValue: Double, fullGainAtLowValue: Double, fullGainAtHighValue: Double, lowFadeCurveType: PHASECurveType, highFadeCurveType: PHASECurveType, subtree: PHASESoundEventNodeDefinition)Adds a child node that blends between a given high and low value.

### addRangeForInputValuesAbove(value:fullGainAtValue:fadeCurveType:subtree:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseblendnodedefinition/addrangeforinputvaluesabove(value:fullgainatvalue:fadecurvetype:subtree:)

PHASE  PHASEBlendNodeDefinition  addRangeForInputValuesAbove(value:fullGainAtValue:fadeCurveType:subtree:) Instance MethodaddRangeForInputValuesAbove(value:fullGainAtValue:fadeCurveType:subtree:)Adds a child node that blends above a given value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func addRangeForInputValuesAbove(
    value: Double,
    fullGainAtValue: Double,
    fadeCurveType: PHASECurveType,
    subtree: PHASESoundEventNodeDefinition
) Parameters valueThe value below which the child node blends.fullGainAtValueA threshold such that the node applies a fade curve to the child node’s gain when the blend parameter is between value and this value.fadeCurveTypeAn option that determines a rate of change for the child node’s gain over the fade range.subtreeA child node to blend.See AlsoAdding Child Nodesfunc addRange(envelope: PHASEEnvelope, subtree: PHASESoundEventNodeDefinition)Adds a child node with an envelope.func addRangeForInputValuesBelow(value: Double, fullGainAtValue: Double, fadeCurveType: PHASECurveType, subtree: PHASESoundEventNodeDefinition)Adds a child node that blends below a given value.func addRangeForInputValuesBetween(lowValue: Double, highValue: Double, fullGainAtLowValue: Double, fullGainAtHighValue: Double, lowFadeCurveType: PHASECurveType, highFadeCurveType: PHASECurveType, subtree: PHASESoundEventNodeDefinition)Adds a child node that blends between a given high and low value.

### addRangeForInputValuesBelow(value:fullGainAtValue:fadeCurveType:subtree:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseblendnodedefinition/addrangeforinputvaluesbelow(value:fullgainatvalue:fadecurvetype:subtree:)

PHASE  PHASEBlendNodeDefinition  addRangeForInputValuesBelow(value:fullGainAtValue:fadeCurveType:subtree:) Instance MethodaddRangeForInputValuesBelow(value:fullGainAtValue:fadeCurveType:subtree:)Adds a child node that blends below a given value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func addRangeForInputValuesBelow(
    value: Double,
    fullGainAtValue: Double,
    fadeCurveType: PHASECurveType,
    subtree: PHASESoundEventNodeDefinition
) Parameters valueThe value above which the child node blends.fullGainAtValueA threshold such that the node applies a fade curve to the child node’s gain when the blend parameter is between value and this value.fadeCurveTypeAn option that determines a rate of change for the child node’s gain over the fade range.subtreeA child node to blend.See AlsoAdding Child Nodesfunc addRange(envelope: PHASEEnvelope, subtree: PHASESoundEventNodeDefinition)Adds a child node with an envelope.func addRangeForInputValuesAbove(value: Double, fullGainAtValue: Double, fadeCurveType: PHASECurveType, subtree: PHASESoundEventNodeDefinition)Adds a child node that blends above a given value.func addRangeForInputValuesBetween(lowValue: Double, highValue: Double, fullGainAtLowValue: Double, fullGainAtHighValue: Double, lowFadeCurveType: PHASECurveType, highFadeCurveType: PHASECurveType, subtree: PHASESoundEventNodeDefinition)Adds a child node that blends between a given high and low value.

### addRangeForInputValuesBetween(lowValue:highValue:fullGainAtLowValue:fullGainAtHighValue:lowFadeCurveType:highFadeCurveType:subtree:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseblendnodedefinition/addrangeforinputvaluesbetween(lowvalue:highvalue:fullgainatlowvalue:fullgainathighvalue:lowfadecurvetype:highfadecurvetype:subtree:)

PHASE  PHASEBlendNodeDefinition  addRangeForInputValuesBetween(lowValue:highValue:fullGainAtLowValue:fullGainAtHighValue:lowFadeCurveType:highFadeCurveType:subtree:) Instance MethodaddRangeForInputValuesBetween(lowValue:highValue:fullGainAtLowValue:fullGainAtHighValue:lowFadeCurveType:highFadeCurveType:subtree:)Adds a child node that blends between a given high and low value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func addRangeForInputValuesBetween(
    lowValue: Double,
    highValue: Double,
    fullGainAtLowValue: Double,
    fullGainAtHighValue: Double,
    lowFadeCurveType: PHASECurveType,
    highFadeCurveType: PHASECurveType,
    subtree: PHASESoundEventNodeDefinition
) Parameters lowValueA value above which the child node blends.highValueA value below which the child node blends.fullGainAtLowValueThe threshold for which a fade curve that lowFadeCurveType defines applies to the gain when the blend parameter value is between lowValue and fullGainAtLowValue.fullGainAtHighValueThe threshold for which a fade curve that highFadeCurveType defines applies to the gain when the blend parameter value is between highValue and fullGainAtHighValue.lowFadeCurveTypeAn option that determines a rate of change for the child node’s gain over the low fade range.highFadeCurveTypeAn option that determines a rate of change for the child node’s gain over the high fade range.subtreeA child node to blend.See AlsoAdding Child Nodesfunc addRange(envelope: PHASEEnvelope, subtree: PHASESoundEventNodeDefinition)Adds a child node with an envelope.func addRangeForInputValuesAbove(value: Double, fullGainAtValue: Double, fadeCurveType: PHASECurveType, subtree: PHASESoundEventNodeDefinition)Adds a child node that blends above a given value.func addRangeForInputValuesBelow(value: Double, fullGainAtValue: Double, fadeCurveType: PHASECurveType, subtree: PHASESoundEventNodeDefinition)Adds a child node that blends below a given value.

### blendParameterDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseblendnodedefinition/blendparameterdefinition

PHASE  PHASEBlendNodeDefinition  blendParameterDefinition Instance PropertyblendParameterDefinitionThe meta parameter definition that caps the blend range.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var blendParameterDefinition: PHASENumberMetaParameterDefinition? { get }DiscussionThe framework sets the value of this property to the init(blendMetaParameterDefinition:) argument.See AlsoAccessing Blend Propertiesvar spatialMixerDefinitionForDistance: PHASESpatialMixerDefinition?An object that combines spatial audio layers.

### init(blendMetaParameterDefinition:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseblendnodedefinition/init(blendmetaparameterdefinition:)

PHASE  PHASEBlendNodeDefinition  init(blendMetaParameterDefinition:) Initializerinit(blendMetaParameterDefinition:)Creates a blend node with a maxiumum blend range value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(blendMetaParameterDefinition: PHASENumberMetaParameterDefinition) Parameters blendMetaParameterDefinitionA maximum value for the blend range. The sound event’s blend meta parameter across a range from 0 to this value produces an active cross-fade along the child nodes.See AlsoCreating a Blend Nodeconvenience init(blendMetaParameterDefinition: PHASENumberMetaParameterDefinition, identifier: String)Creates a named blend node with a maxiumum blend range value.init(spatialMixerDefinition: PHASESpatialMixerDefinition)Creates a blend node for spatial audio output.convenience init(spatialMixerDefinition: PHASESpatialMixerDefinition, identifier: String)Creates a named blend node for spatial audio output.

### init(blendMetaParameterDefinition:identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseblendnodedefinition/init(blendmetaparameterdefinition:identifier:)

PHASE  PHASEBlendNodeDefinition  init(blendMetaParameterDefinition:identifier:) Initializerinit(blendMetaParameterDefinition:identifier:)Creates a named blend node with a maxiumum blend range value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+convenience init(
    blendMetaParameterDefinition: PHASENumberMetaParameterDefinition,
    identifier: String
) Parameters blendMetaParameterDefinitionA maximum value for the blend range. The sound event’s blend meta parameter across a range from 0 to this value produces an active cross-fade along the child nodes.identifierA unique name for the blend node.See AlsoCreating a Blend Nodeinit(blendMetaParameterDefinition: PHASENumberMetaParameterDefinition)Creates a blend node with a maxiumum blend range value.init(spatialMixerDefinition: PHASESpatialMixerDefinition)Creates a blend node for spatial audio output.convenience init(spatialMixerDefinition: PHASESpatialMixerDefinition, identifier: String)Creates a named blend node for spatial audio output.

### init(spatialMixerDefinition:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseblendnodedefinition/init(spatialmixerdefinition:)

PHASE  PHASEBlendNodeDefinition  init(spatialMixerDefinition:) Initializerinit(spatialMixerDefinition:)Creates a blend node for spatial audio output.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(spatialMixerDefinition: PHASESpatialMixerDefinition) Parameters spatialMixerDefinitionAn object that combines spatial audio layers.See AlsoCreating a Blend Nodeinit(blendMetaParameterDefinition: PHASENumberMetaParameterDefinition)Creates a blend node with a maxiumum blend range value.convenience init(blendMetaParameterDefinition: PHASENumberMetaParameterDefinition, identifier: String)Creates a named blend node with a maxiumum blend range value.convenience init(spatialMixerDefinition: PHASESpatialMixerDefinition, identifier: String)Creates a named blend node for spatial audio output.

### init(spatialMixerDefinition:identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseblendnodedefinition/init(spatialmixerdefinition:identifier:)

PHASE  PHASEBlendNodeDefinition  init(spatialMixerDefinition:identifier:) Initializerinit(spatialMixerDefinition:identifier:)Creates a named blend node for spatial audio output.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+convenience init(
    spatialMixerDefinition: PHASESpatialMixerDefinition,
    identifier: String
) Parameters spatialMixerDefinitionAn object that combines spatial audio layers.identifierA unique name for the node.See AlsoCreating a Blend Nodeinit(blendMetaParameterDefinition: PHASENumberMetaParameterDefinition)Creates a blend node with a maxiumum blend range value.convenience init(blendMetaParameterDefinition: PHASENumberMetaParameterDefinition, identifier: String)Creates a named blend node with a maxiumum blend range value.init(spatialMixerDefinition: PHASESpatialMixerDefinition)Creates a blend node for spatial audio output.

### spatialMixerDefinitionForDistance | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseblendnodedefinition/spatialmixerdefinitionfordistance

PHASE  PHASEBlendNodeDefinition  spatialMixerDefinitionForDistance Instance PropertyspatialMixerDefinitionForDistanceAn object that combines spatial audio layers.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var spatialMixerDefinitionForDistance: PHASESpatialMixerDefinition? { get }DiscussionThe framework sets this property to the init(spatialMixerDefinition:) argument.See AlsoAccessing Blend Propertiesvar blendParameterDefinition: PHASENumberMetaParameterDefinition?The meta parameter definition that caps the blend range.

## PHASECalibrationMode | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecalibrationmode

PHASE  PHASECalibrationMode EnumerationPHASECalibrationModeCalibration options for sound pressure level.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum PHASECalibrationModeTopicsModescase absoluteSplA sound pressure level based on the current output device.case noneAn option that specifies no loudness calibration.case relativeSplA sound pressure level that’s tuned for the device.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoAudio-Providing Nodesclass PHASESamplerNodeDefinitionA node that plays complete audio data.enum PHASEPlaybackModeLoop options for audio playback.class PHASEPushStreamNodeDefinitionA node that plays a sequence of audio buffers.class PHASEPushStreamNodeAn audio stream you manage to provide a sound buffer data.struct PHASEPushStreamBufferOptionsOptions that inform PHASE of an audio-stream buffer’s playback priority.class PHASEGeneratorNodeDefinitionA base class for nodes that provide audio data to generate sound.

### PHASECalibrationMode.absoluteSpl | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecalibrationmode/absolutespl

PHASE  PHASECalibrationMode  PHASECalibrationMode.absoluteSpl CasePHASECalibrationMode.absoluteSplA sound pressure level based on the current output device.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case absoluteSplSee AlsoModescase noneAn option that specifies no loudness calibration.case relativeSplA sound pressure level that’s tuned for the device.

### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecalibrationmode/init(rawvalue:)

PHASE  PHASECalibrationMode  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

### PHASECalibrationMode.none | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecalibrationmode/none

PHASE  PHASECalibrationMode  PHASECalibrationMode.none CasePHASECalibrationMode.noneAn option that specifies no loudness calibration.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case noneDiscussionFor a consistent user experience across platforms and output devices, avoid PHASECalibrationMode.none by correcting loudness with PHASECalibrationMode.absoluteSpl or PHASECalibrationMode.relativeSpl.See AlsoModescase absoluteSplA sound pressure level based on the current output device.case relativeSplA sound pressure level that’s tuned for the device.

### PHASECalibrationMode.relativeSpl | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecalibrationmode/relativespl

PHASE  PHASECalibrationMode  PHASECalibrationMode.relativeSpl CasePHASECalibrationMode.relativeSplA sound pressure level that’s tuned for the device.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case relativeSplSee AlsoModescase absoluteSplA sound pressure level based on the current output device.case noneAn option that specifies no loudness calibration.

## PHASECardioidDirectivityModelParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecardioiddirectivitymodelparameters

PHASE  PHASECardioidDirectivityModelParameters ClassPHASECardioidDirectivityModelParametersAn object that directs sound in a heart-shaped curve surrounding a sound source.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASECardioidDirectivityModelParametersOverviewThis class configures a particular frequency range in the audio spectrum that emits sound in an area defined by a mathematical cardioid. PHASE refers to each frequency segment along the audio spectrum as a subband. This class contains an array of subbands that each can direct sound in a unique cardioid shape. The framework outputs a blend of a frequency’s adjacent subbands for all frequencies that lie outside of those specified in the subbands array.Emit Sound in the Shape of a CardioidThe following code defines a two-band cardioid model. The first subband resembles a heart-shaped cardioid and the second resembles a hypercardioid.let simpleCardioid = PHASECardioidDirectivityModelParameters()

// Create a cardioid model.
var cardioidSegment1 = PHASECardioidDirectivityModelSubbandParameters()
cardioidSegment1.frequency = 500.0
cardioidSegment1.pattern = 0.5 // Cardioid shape
cardioidSegment1.sharpness = 1.0

// Create a hypercardioid model.
var cardioidSegment2 = PHASECardioidDirectivityModelSubbandParameters()
cardioidSegment2.frequency = 5000.0
cardioidSegment2.pattern = 0.75
cardioidSegment2.sharpness = 1.5

simpleCardioid.subbands.add(cardioidSegment1)
simpleCardioid.subbands.add(cardioidSegment2)

spatialMixer.sourceDirectivityModelParameters = simpleCardioid
PHASECardioidDirectivityModelParameters* simpleCardioid = [[PHASECardioidDirectivityModelParameters alloc] init];

// Create a cardioid model.
PHASECardioidDirectivityModelSubbandParameters* cardioidSegment1 = [[PHASECardioidDirectivityModelSubbandParameters alloc] init];
cardioidSegment1.frequency = 500.f;
cardioidSegment1.pattern = .5f; 
cardioidSegment1.sharpness = 1.f;

// Create a hypercardioid model.
PHASECardioidDirectivityModelSubbandParameters* cardioidSegment2 = [[PHASECardioidDirectivityModelSubbandParameters alloc] init];
cardioidSegment2.frequency = 5000.f;
cardioidSegment2.pattern = .75f;
cardioidSegment2.sharpness = 1.5f;

[simpleCardioid.subbands addObject:cardioidSegment1];
[simpleCardioid.subbands addObject:cardioidSegment2];

spatialMixer.sourceDirectivityModelParameters = simpleCardioid;
TopicsCreating the Cardioid Directivity Model Parametersinit(subbandParameters: [PHASECardioidDirectivityModelSubbandParameters])Creates an object that directs sound in a heart-shaped curve surrounding a sound source.Defining Subbandsvar subbandParameters: [PHASECardioidDirectivityModelSubbandParameters]An array of frequencies that describe varying sound emission across the spectrum.RelationshipsInherits FromPHASEDirectivityModelParametersConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSound Directivityclass PHASECardioidDirectivityModelSubbandParametersA data set that projects sound of a certain frequency outward in the shape of a heart.class PHASEConeDirectivityModelParametersAn object that directs sound in a cone-shaped curve that extends from a sound source.class PHASEConeDirectivityModelSubbandParametersA data set that projects sound of a certain frequency outward in the shape of a cone.class PHASEDirectivityModelParametersA base class for objects that direct sound.

### init(subbandParameters:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecardioiddirectivitymodelparameters/init(subbandparameters:)

PHASE  PHASECardioidDirectivityModelParameters  init(subbandParameters:) Initializerinit(subbandParameters:)Creates an object that directs sound in a heart-shaped curve surrounding a sound source.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(subbandParameters: [PHASECardioidDirectivityModelSubbandParameters]) Parameters subbandParametersAn array of frequencies that describe varying sound emission across the spectrum.

### subbandParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecardioiddirectivitymodelparameters/subbandparameters

PHASE  PHASECardioidDirectivityModelParameters  subbandParameters Instance PropertysubbandParametersAn array of frequencies that describe varying sound emission across the spectrum.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var subbandParameters: [PHASECardioidDirectivityModelSubbandParameters] { get }DiscussionThis property is read only. The framework sets the value to the argument you supply the init(subbandParameters:) initializer.

## PHASECardioidDirectivityModelSubbandParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecardioiddirectivitymodelsubbandparameters

PHASE  PHASECardioidDirectivityModelSubbandParameters ClassPHASECardioidDirectivityModelSubbandParametersA data set that projects sound of a certain frequency outward in the shape of a heart.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASECardioidDirectivityModelSubbandParametersOverviewThis class defines one subband in the PHASECardioidDirectivityModelParameters class’s subbands. Depending on the specific shape you define with pattern and sharpness, you can attenuate sound focused at frequency to the sides of the listener, while leaving the sound in front of or behind the listener unchanged.TopicsCreating Cardioid Directivity Subband Parametersinit()Creates a data set that projects sound of a certain frequency outward in the shape of a heart.Sizing the Subbandvar frequency: DoubleA frequency in the audio spectrum where the pattern and sharpness resonate most.Shaping Directivityvar pattern: DoubleA shape that determines the direction of sound.var sharpness: DoubleThe amount that the shape overlaps with bordering subbands.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSound Directivityclass PHASECardioidDirectivityModelParametersAn object that directs sound in a heart-shaped curve surrounding a sound source.class PHASEConeDirectivityModelParametersAn object that directs sound in a cone-shaped curve that extends from a sound source.class PHASEConeDirectivityModelSubbandParametersA data set that projects sound of a certain frequency outward in the shape of a cone.class PHASEDirectivityModelParametersA base class for objects that direct sound.

### frequency | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecardioiddirectivitymodelsubbandparameters/frequency

PHASE  PHASECardioidDirectivityModelSubbandParameters  frequency Instance PropertyfrequencyA frequency in the audio spectrum where the pattern and sharpness resonate most.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var frequency: Double { get set }DiscussionThe default value is 1000.0.

### init() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecardioiddirectivitymodelsubbandparameters/init()

PHASE  PHASECardioidDirectivityModelSubbandParameters  init() Initializerinit()Creates a data set that projects sound of a certain frequency outward in the shape of a heart.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init()

### pattern | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecardioiddirectivitymodelsubbandparameters/pattern

PHASE  PHASECardioidDirectivityModelSubbandParameters  pattern Instance PropertypatternA shape that determines the direction of sound.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var pattern: Double { get set }DiscussionThe framework clamps the value to the range [0.0, 1.0]. The default value is 0.0, which creates an omnidirectional shape. The value 0.5 creates a cardioid shape. The value 1.0 creates a dipole shape.See AlsoShaping Directivityvar sharpness: DoubleThe amount that the shape overlaps with bordering subbands.

### sharpness | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecardioiddirectivitymodelsubbandparameters/sharpness

PHASE  PHASECardioidDirectivityModelSubbandParameters  sharpness Instance PropertysharpnessThe amount that the shape overlaps with bordering subbands.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var sharpness: Double { get set }DiscussionThis property condenses the shape of the pattern such that higher values extend the shape frontwards. Increasing sharpness for dipole (a pattern value of 1.0), extends the shape frontwards and backwards.The default value is 1.0. Values greater than 1.0 increase sharpness. The framework clamps the value to the range [1.0, greatestFiniteMagnitude].See AlsoShaping Directivityvar pattern: DoubleA shape that determines the direction of sound.

## PHASEChannelMixerDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasechannelmixerdefinition

PHASE  PHASEChannelMixerDefinition ClassPHASEChannelMixerDefinitionAn audio-layering object that routes sound directly to the device’s output.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEChannelMixerDefinitionOverviewUse this class to play one-time sounds such as menu clicks.Note If your audio playback requires 3D orienting or positioning, use PHASEAmbientMixerDefinition or PHASESpatialMixerDefinition, respectively. For more information, see Spatial Mixing.This class defines the channel routing, which is the strategy the framework uses to send source mono or multichannel assets to the output for playback. The asset’s audio channels route to the output for playback according to the channel layout and runtime output conditions the app designates on an instance of this class.This class minimizes up mixing and down mixing — that is, source audio channel conversion to a higher or lower number of channels. For example, although a spatial mixer overrides the use of output channels by panning to convey listener position and orientation, the channel mixer maintains source audio channel layout to preserve the listening experience of the source audio.TopicsCreating a Channel Mixerinit(channelLayout: AVAudioChannelLayout)Creates a channel mixer with the given channel layout.convenience init(channelLayout: AVAudioChannelLayout, identifier: String)Creates a named channel mixer with the given channel layout.Inspecting Channel Layoutvar inputChannelLayout: AVAudioChannelLayoutThe channel layout of the mixer’s input audio.RelationshipsInherits FromPHASEMixerDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoAudio Layering and Effectsclass PHASEAmbientMixerDefinitionAn audio-layering object that outputs sound in a particular direction in 3D space.class PHASEMixerDefinitionAn object to initialize a mixer with a given configuration.class PHASEMixerAn object that combines multiple audio signals into a single signal.class PHASEDefinitionA base class that adds a name to framework definitions.API ReferenceSpatial MixingDefine environmental characteristics that determine how sound plays in your app’s 3D soundscape.

### init(channelLayout:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasechannelmixerdefinition/init(channellayout:)

PHASE  PHASEChannelMixerDefinition  init(channelLayout:) Initializerinit(channelLayout:)Creates a channel mixer with the given channel layout.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(channelLayout layout: AVAudioChannelLayout) Parameters layoutA channel configuration for the mixer’s input audio.See AlsoCreating a Channel Mixerconvenience init(channelLayout: AVAudioChannelLayout, identifier: String)Creates a named channel mixer with the given channel layout.

### init(channelLayout:identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasechannelmixerdefinition/init(channellayout:identifier:)

PHASE  PHASEChannelMixerDefinition  init(channelLayout:identifier:) Initializerinit(channelLayout:identifier:)Creates a named channel mixer with the given channel layout.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+convenience init(
    channelLayout layout: AVAudioChannelLayout,
    identifier: String
) Parameters layoutA channel configuration for the mixer’s input audio.identifierA unique name for the channel mixer.See AlsoCreating a Channel Mixerinit(channelLayout: AVAudioChannelLayout)Creates a channel mixer with the given channel layout.

### inputChannelLayout | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasechannelmixerdefinition/inputchannellayout

PHASE  PHASEChannelMixerDefinition  inputChannelLayout Instance PropertyinputChannelLayoutThe channel layout of the mixer’s input audio.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var inputChannelLayout: AVAudioChannelLayout { get }

## PHASEConeDirectivityModelParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseconedirectivitymodelparameters

PHASE  PHASEConeDirectivityModelParameters ClassPHASEConeDirectivityModelParametersAn object that directs sound in a cone-shaped curve that extends from a sound source.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEConeDirectivityModelParametersOverviewThis class determines that a particular frequency range in the audio spectrum emits sound in an area defined by a mathematical cone. PHASE refers to each frequency segment along the audio spectrum as a subband. This class contains an array of subbands that each direct sound in a unique cone shape. The framework outputs a blend of a frequency’s adjacent subbands for all frequencies that lie outside of those specified in the subbands array.Emit Sound in the Shape of a ConeThe following code defines a cone directivity model with two subbands. The first subband emits sound in a narrow region and the second subband outputs sound in a wider region.let simpleCone = PHASEConeDirectivityModelParameters()

let coneSegment1 = PHASEConeDirectivityModelSubbandParameters()
coneSegment1.frequency = 500.0
coneSegment1.innerAngle = 60.0
coneSegment1.outerAngle = 80.0
coneSegment1.outerGain = 0.5

let coneSegment2 = PHASEConeDirectivityModelSubbandParameters()
coneSegment2.frequency = 5000.0
coneSegment2.innerAngle = 30.0
coneSegment2.outerAngle = 40.0
coneSegment2.outerGain = 0.3

simpleCone.subbands.add(coneSegment1)
simpleCone.subbands.add(coneSegment2)

spatialMixer.listenerDirectivityModelParameters = simpleCone
PHASEConeDirectivityModelParameters* simpleCone = 
    [[PHASEConeDirectivityModelParameters alloc] init];

PHASEConeDirectivityModelSubbandParameters* coneSegment1 = 
    [[PHASEConeDirectivityModelSubbandParameters alloc] init];
coneSegment1.frequency = 5000.f;
coneSegment1.innerAngle = 30.f;
coneSegment1.outerAngle = 40.f;
coneSegment1.outerGain = .3f;

PHASEConeDirectivityModelSubbandParameters* coneSegment2 = 
    [[PHASEConeDirectivityModelSubbandParameters alloc] init];
coneSegment2.frequency = 500.f;
coneSegment2.innerAngle = 60.f;
coneSegment2.outerAngle = 80.f;
coneSegment2.outerGain = .5f;

[simpleCone.subbands addObject:coneSegment1];
[simpleCone.subbands addObject:coneSegment2];

spatialMixer.listenerDirectivityModelParameters = simpleCone;
TopicsCreating the Cone Directivity Model Parametersinit(subbandParameters: [PHASEConeDirectivityModelSubbandParameters])Creates an object that directs sound in a cone-shaped curve that extends from a sound source.Defining Subbandsvar subbandParameters: [PHASEConeDirectivityModelSubbandParameters]An array of frequencies that describe varying sound emission across the spectrum.RelationshipsInherits FromPHASEDirectivityModelParametersConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSound Directivityclass PHASECardioidDirectivityModelParametersAn object that directs sound in a heart-shaped curve surrounding a sound source.class PHASECardioidDirectivityModelSubbandParametersA data set that projects sound of a certain frequency outward in the shape of a heart.class PHASEConeDirectivityModelSubbandParametersA data set that projects sound of a certain frequency outward in the shape of a cone.class PHASEDirectivityModelParametersA base class for objects that direct sound.

### init(subbandParameters:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseconedirectivitymodelparameters/init(subbandparameters:)

PHASE  PHASEConeDirectivityModelParameters  init(subbandParameters:) Initializerinit(subbandParameters:)Creates an object that directs sound in a cone-shaped curve that extends from a sound source.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(subbandParameters: [PHASEConeDirectivityModelSubbandParameters]) Parameters subbandParametersAn array of frequencies that describe varying sound emission across the spectrum.

### subbandParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseconedirectivitymodelparameters/subbandparameters

PHASE  PHASEConeDirectivityModelParameters  subbandParameters Instance PropertysubbandParametersAn array of frequencies that describe varying sound emission across the spectrum.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var subbandParameters: [PHASEConeDirectivityModelSubbandParameters] { get }DiscussionThis property is read only. The framework sets the value to the argument you supply the init(subbandParameters:) initializer.

## PHASEConeDirectivityModelSubbandParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseconedirectivitymodelsubbandparameters

PHASE  PHASEConeDirectivityModelSubbandParameters ClassPHASEConeDirectivityModelSubbandParametersA data set that projects sound of a certain frequency outward in the shape of a cone.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEConeDirectivityModelSubbandParametersOverviewThis class defines one subband in the PHASEConeDirectivityModelParameters class’s subbands. The inner and outer angles you define with setAngles(innerAngle:outerAngle:) describe a cone that directs sound of a given frequency toward the listener. The cone’s point rests at the 3D position of the sound source. The framework adjusts the volume of the sound according to location of the listener in the 3D scene:If the listener positions in an area outside of the subband’s outerAngle, the sound emanates from the source at the volume defined by outerGain.If the listener positions inside the area defined by innerAngle, the sound emanates from the source at maximum volume.If the listener positions in between the outer and inner angles, the framework blends the volume to a value between outerGain and the maximum.TopicsCreating Cone Directivity Subband Parametersinit()Creates a data set that projects sound of a certain frequency outward in the shape of a cone.Sizing the Subbandvar frequency: DoubleA frequency in the audio spectrum where the subband resonates most.Shaping Directivityvar innerAngle: DoubleAn angle, in degrees, that determines the size of the audio emitting area inside the cone.var outerAngle: DoubleAn angle, in degrees, that determines the size of the audio emitting area outside the cone.var outerGain: DoubleThe loudness of the audio the outside area of the cone emits.func setAngles(innerAngle: Double, outerAngle: Double)Configures a focus area for cone-based sound directivity.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSound Directivityclass PHASECardioidDirectivityModelParametersAn object that directs sound in a heart-shaped curve surrounding a sound source.class PHASECardioidDirectivityModelSubbandParametersA data set that projects sound of a certain frequency outward in the shape of a heart.class PHASEConeDirectivityModelParametersAn object that directs sound in a cone-shaped curve that extends from a sound source.class PHASEDirectivityModelParametersA base class for objects that direct sound.

### Web Server Error
*Source:* https://developer.apple.com/documentation/phase/phaseconedirectivitymodelsubbandparameters/frequency

Web Server Error

Description: The host did not return the document correctly.

### init() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseconedirectivitymodelsubbandparameters/init()

PHASE  PHASEConeDirectivityModelSubbandParameters  init() Initializerinit()Creates a data set that projects sound of a certain frequency outward in the shape of a cone.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init()

### innerAngle | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseconedirectivitymodelsubbandparameters/innerangle

PHASE  PHASEConeDirectivityModelSubbandParameters  innerAngle Instance PropertyinnerAngleAn angle, in degrees, that determines the size of the audio emitting area inside the cone.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var innerAngle: Double { get }DiscussionTo set this property, call setAngles(innerAngle:outerAngle:).See AlsoShaping Directivityvar outerAngle: DoubleAn angle, in degrees, that determines the size of the audio emitting area outside the cone.var outerGain: DoubleThe loudness of the audio the outside area of the cone emits.func setAngles(innerAngle: Double, outerAngle: Double)Configures a focus area for cone-based sound directivity.

### outerAngle | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseconedirectivitymodelsubbandparameters/outerangle

PHASE  PHASEConeDirectivityModelSubbandParameters  outerAngle Instance PropertyouterAngleAn angle, in degrees, that determines the size of the audio emitting area outside the cone.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var outerAngle: Double { get }DiscussionTo set this property, call setAngles(innerAngle:outerAngle:).See AlsoShaping Directivityvar innerAngle: DoubleAn angle, in degrees, that determines the size of the audio emitting area inside the cone.var outerGain: DoubleThe loudness of the audio the outside area of the cone emits.func setAngles(innerAngle: Double, outerAngle: Double)Configures a focus area for cone-based sound directivity.

### outerGain | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseconedirectivitymodelsubbandparameters/outergain

PHASE  PHASEConeDirectivityModelSubbandParameters  outerGain Instance PropertyouterGainThe loudness of the audio the outside area of the cone emits.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var outerGain: Double { get set }DiscussionThe framework clamps the value of this property to the range [0, 1], where 0 silences loudness and 1 doesn’t modify loudness.See AlsoShaping Directivityvar innerAngle: DoubleAn angle, in degrees, that determines the size of the audio emitting area inside the cone.var outerAngle: DoubleAn angle, in degrees, that determines the size of the audio emitting area outside the cone.func setAngles(innerAngle: Double, outerAngle: Double)Configures a focus area for cone-based sound directivity.

### setAngles(innerAngle:outerAngle:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseconedirectivitymodelsubbandparameters/setangles(innerangle:outerangle:)

PHASE  PHASEConeDirectivityModelSubbandParameters  setAngles(innerAngle:outerAngle:) Instance MethodsetAngles(innerAngle:outerAngle:)Configures a focus area for cone-based sound directivity.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func setAngles(
    innerAngle: Double,
    outerAngle: Double
) Parameters innerAngleAn angle that determines the size of the audio emitting area inside the cone.outerAngleAn angle that determines the size of the audio emitting area outside the cone.DiscussionThe default value for each angle is 360.0. The outer angle needs to be greater than or equal to the inner angle.See AlsoShaping Directivityvar innerAngle: DoubleAn angle, in degrees, that determines the size of the audio emitting area inside the cone.var outerAngle: DoubleAn angle, in degrees, that determines the size of the audio emitting area outside the cone.var outerGain: DoubleThe loudness of the audio the outside area of the cone emits.

## PHASEContainerNodeDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecontainernodedefinition

PHASE  PHASEContainerNodeDefinition ClassPHASEContainerNodeDefinitionA node that plays all its children at the same time.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEContainerNodeDefinitionOverviewThis node adds structure to the sound event tree while performing no conditional logic or audio playback of its own. By passing invocation to all its children at once, this class invokes the child nodes’ actions simultaneously.TopicsCreating a Nodeinit()Creates a container node.init(identifier: String)Creates a container node with the given name.class func new() -> SelfCreates a container node.Adding Descendent Nodesfunc addSubtree(PHASESoundEventNodeDefinition)Adds a sound event node as a child.RelationshipsInherits FromPHASESoundEventNodeDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoControl Nodesclass PHASESwitchNodeDefinitionA node that passes invocation to only one of its child nodes.class PHASERandomNodeDefinitionA sound event node that invokes one of its child nodes at random.class PHASEBlendNodeDefinitionA node that smoothly fades between the audio of its child nodes.

### addSubtree(_:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecontainernodedefinition/addsubtree(_:)

PHASE  PHASEContainerNodeDefinition  addSubtree(_:) Instance MethodaddSubtree(_:)Adds a sound event node as a child.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func addSubtree(_ subtree: PHASESoundEventNodeDefinition) Parameters subtreeThe child node, which itself can contain a hierarchical tree of descendent nodes.

### init() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecontainernodedefinition/init()

PHASE  PHASEContainerNodeDefinition  init() Initializerinit()Creates a container node.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init()See AlsoCreating a Nodeinit(identifier: String)Creates a container node with the given name.class func new() -> SelfCreates a container node.

### init(identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecontainernodedefinition/init(identifier:)

PHASE  PHASEContainerNodeDefinition  init(identifier:) Initializerinit(identifier:)Creates a container node with the given name.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(identifier: String) Parameters identifierA unique name for the node.See AlsoCreating a Nodeinit()Creates a container node.class func new() -> SelfCreates a container node.

### new() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecontainernodedefinition/new()

PHASE  PHASEContainerNodeDefinition  new() Type Methodnew()Creates a container node.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class func new() -> SelfSee AlsoCreating a Nodeinit()Creates a container node.init(identifier: String)Creates a container node with the given name.

## PHASECullOption | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseculloption

PHASE  PHASECullOption EnumerationPHASECullOptionThe actions the engine takes when it culls sound.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum PHASECullOptionOverviewCulling refers to the temporary removal of a sound from the audio output. This enumeration determines the actions a sampler node performs after the engine culls its sound or queues it for culling. To indicate a preference, the app sets a sampler node’s cullOption property.TopicsOptionscase terminateAn option that culls sound by stopping playback.case doNotCullAn option that indicates the framework takes no action to cull sound.case sleepWakeAtRealtimeOffsetAn option that pauses playback and resumes where it left off.case sleepWakeAtZeroAn option that pauses playback and resumes at the beginning.case sleepWakeAtRandomOffsetAn option that pauses playback and resumes at a random position.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoDefining Cull Behaviorvar cullOption: PHASECullOptionThe action the engine performs after it temporarily removes the node’s sound from the audio output.

### PHASECullOption.doNotCull | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseculloption/donotcull

PHASE  PHASECullOption  PHASECullOption.doNotCull CasePHASECullOption.doNotCullAn option that indicates the framework takes no action to cull sound.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case doNotCullSee AlsoOptionscase terminateAn option that culls sound by stopping playback.case sleepWakeAtRealtimeOffsetAn option that pauses playback and resumes where it left off.case sleepWakeAtZeroAn option that pauses playback and resumes at the beginning.case sleepWakeAtRandomOffsetAn option that pauses playback and resumes at a random position.

### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseculloption/init(rawvalue:)

PHASE  PHASECullOption  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

### PHASECullOption.sleepWakeAtRandomOffset | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseculloption/sleepwakeatrandomoffset

PHASE  PHASECullOption  PHASECullOption.sleepWakeAtRandomOffset CasePHASECullOption.sleepWakeAtRandomOffsetAn option that pauses playback and resumes at a random position.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case sleepWakeAtRandomOffsetSee AlsoOptionscase terminateAn option that culls sound by stopping playback.case doNotCullAn option that indicates the framework takes no action to cull sound.case sleepWakeAtRealtimeOffsetAn option that pauses playback and resumes where it left off.case sleepWakeAtZeroAn option that pauses playback and resumes at the beginning.

### PHASECullOption.sleepWakeAtRealtimeOffset | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseculloption/sleepwakeatrealtimeoffset

PHASE  PHASECullOption  PHASECullOption.sleepWakeAtRealtimeOffset CasePHASECullOption.sleepWakeAtRealtimeOffsetAn option that pauses playback and resumes where it left off.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case sleepWakeAtRealtimeOffsetSee AlsoOptionscase terminateAn option that culls sound by stopping playback.case doNotCullAn option that indicates the framework takes no action to cull sound.case sleepWakeAtZeroAn option that pauses playback and resumes at the beginning.case sleepWakeAtRandomOffsetAn option that pauses playback and resumes at a random position.

### PHASECullOption.sleepWakeAtZero | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseculloption/sleepwakeatzero

PHASE  PHASECullOption  PHASECullOption.sleepWakeAtZero CasePHASECullOption.sleepWakeAtZeroAn option that pauses playback and resumes at the beginning.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case sleepWakeAtZeroSee AlsoOptionscase terminateAn option that culls sound by stopping playback.case doNotCullAn option that indicates the framework takes no action to cull sound.case sleepWakeAtRealtimeOffsetAn option that pauses playback and resumes where it left off.case sleepWakeAtRandomOffsetAn option that pauses playback and resumes at a random position.

### PHASECullOption.terminate | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseculloption/terminate

PHASE  PHASECullOption  PHASECullOption.terminate CasePHASECullOption.terminateAn option that culls sound by stopping playback.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case terminateSee AlsoOptionscase doNotCullAn option that indicates the framework takes no action to cull sound.case sleepWakeAtRealtimeOffsetAn option that pauses playback and resumes where it left off.case sleepWakeAtZeroAn option that pauses playback and resumes at the beginning.case sleepWakeAtRandomOffsetAn option that pauses playback and resumes at a random position.

## PHASECurveType | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecurvetype

PHASE  PHASECurveType EnumerationPHASECurveTypeOptions that apply a mathematical function to an input value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum PHASECurveTypeOverviewPHASE applies curves in several places across the framework:A PHASEEnvelopeSegment object represents one curved portion of an envelope’s graph.The PHASEGroup class applies a curve type to its sounds by fading its volume with the fadeGain(gain:duration:curveType:) function, and to its rate, with fadeRate(rate:duration:curveType:).Each PHASEGroupPresetSetting applies a curve to control a setting’s rate of change.Apply a Curve as a Rate of ChangeIn most cases, PHASE applies curves to output a rate of change. For example, an  envelope segment’s curveType determines where along the segment’s domain the y-value changes more quickly. The following figure compares all the curves’ rate of change by plotting their input over the range (0,0) to (1,1).TopicsTypescase linearA curve that increases uniformly with its input.case squaredA curve that increases at a rate that squares its input.case inverseSquaredA curve that increases at a rate of one divided by the input’s square.case cubedA curve that increases at a rate that cubes its input.case inverseCubedA curve that increases at a rate of one divided by the input’s cube.case sineA sine curve.case inverseSineAn inverse sine curve.case sigmoidA sigmoid curve.case inverseSigmoidAn inverse sigmoid curve.case holdStartValueA curve that equals its start value for the entire duration.case jumpToEndValueA curve that equals its end value for the entire duration.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoDynamic Sound Controlclass PHASEEnvelopeA collection of segments that connect to graph a complex curve over a linear input.class PHASEEnvelopeSegmentA curved portion of an envelope.class PHASENumericPairAn ordered pair that defines a bounding box for an envelope.API ReferencePlayback ParameterizationChange the characteristics of in-flight audio by adjusting its properties at runtime.

### PHASECurveType.cubed | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecurvetype/cubed

PHASE  PHASECurveType  PHASECurveType.cubed CasePHASECurveType.cubedA curve that increases at a rate that cubes its input.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case cubedDiscussionThe function y = x^3 shapes this curve.See AlsoTypescase linearA curve that increases uniformly with its input.case squaredA curve that increases at a rate that squares its input.case inverseSquaredA curve that increases at a rate of one divided by the input’s square.case inverseCubedA curve that increases at a rate of one divided by the input’s cube.case sineA sine curve.case inverseSineAn inverse sine curve.case sigmoidA sigmoid curve.case inverseSigmoidAn inverse sigmoid curve.case holdStartValueA curve that equals its start value for the entire duration.case jumpToEndValueA curve that equals its end value for the entire duration.

### PHASECurveType.holdStartValue | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecurvetype/holdstartvalue

PHASE  PHASECurveType  PHASECurveType.holdStartValue CasePHASECurveType.holdStartValueA curve that equals its start value for the entire duration.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case holdStartValueDiscussionUse this type for step function curves, such as when mapping a continuously varying input value to a discrete set of output values.See AlsoTypescase linearA curve that increases uniformly with its input.case squaredA curve that increases at a rate that squares its input.case inverseSquaredA curve that increases at a rate of one divided by the input’s square.case cubedA curve that increases at a rate that cubes its input.case inverseCubedA curve that increases at a rate of one divided by the input’s cube.case sineA sine curve.case inverseSineAn inverse sine curve.case sigmoidA sigmoid curve.case inverseSigmoidAn inverse sigmoid curve.case jumpToEndValueA curve that equals its end value for the entire duration.

### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecurvetype/init(rawvalue:)

PHASE  PHASECurveType  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

### PHASECurveType.inverseCubed | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecurvetype/inversecubed

PHASE  PHASECurveType  PHASECurveType.inverseCubed CasePHASECurveType.inverseCubedA curve that increases at a rate of one divided by the input’s cube.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case inverseCubedDiscussionThe function y = 1 / x^3 shapes this curve.See AlsoTypescase linearA curve that increases uniformly with its input.case squaredA curve that increases at a rate that squares its input.case inverseSquaredA curve that increases at a rate of one divided by the input’s square.case cubedA curve that increases at a rate that cubes its input.case sineA sine curve.case inverseSineAn inverse sine curve.case sigmoidA sigmoid curve.case inverseSigmoidAn inverse sigmoid curve.case holdStartValueA curve that equals its start value for the entire duration.case jumpToEndValueA curve that equals its end value for the entire duration.

### PHASECurveType.inverseSigmoid | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecurvetype/inversesigmoid

PHASE  PHASECurveType  PHASECurveType.inverseSigmoid CasePHASECurveType.inverseSigmoidAn inverse sigmoid curve.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case inverseSigmoidDiscussionAlso known as an inverse s-curve, the inverse sigmoid curve’s path movement is quick at either end and slow in the middle.See AlsoTypescase linearA curve that increases uniformly with its input.case squaredA curve that increases at a rate that squares its input.case inverseSquaredA curve that increases at a rate of one divided by the input’s square.case cubedA curve that increases at a rate that cubes its input.case inverseCubedA curve that increases at a rate of one divided by the input’s cube.case sineA sine curve.case inverseSineAn inverse sine curve.case sigmoidA sigmoid curve.case holdStartValueA curve that equals its start value for the entire duration.case jumpToEndValueA curve that equals its end value for the entire duration.

### PHASECurveType.inverseSine | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecurvetype/inversesine

PHASE  PHASECurveType  PHASECurveType.inverseSine CasePHASECurveType.inverseSineAn inverse sine curve.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case inverseSineDiscussionThe function y = sin^-1(x) shapes this curve. The inverse sine curve behaves like PHASECurveType.sine, only rotated 90 degrees.See AlsoTypescase linearA curve that increases uniformly with its input.case squaredA curve that increases at a rate that squares its input.case inverseSquaredA curve that increases at a rate of one divided by the input’s square.case cubedA curve that increases at a rate that cubes its input.case inverseCubedA curve that increases at a rate of one divided by the input’s cube.case sineA sine curve.case sigmoidA sigmoid curve.case inverseSigmoidAn inverse sigmoid curve.case holdStartValueA curve that equals its start value for the entire duration.case jumpToEndValueA curve that equals its end value for the entire duration.

### PHASECurveType.inverseSquared | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecurvetype/inversesquared

PHASE  PHASECurveType  PHASECurveType.inverseSquared CasePHASECurveType.inverseSquaredA curve that increases at a rate of one divided by the input’s square.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case inverseSquaredDiscussionThe function y = 1 / x^2 shapes this curve.See AlsoTypescase linearA curve that increases uniformly with its input.case squaredA curve that increases at a rate that squares its input.case cubedA curve that increases at a rate that cubes its input.case inverseCubedA curve that increases at a rate of one divided by the input’s cube.case sineA sine curve.case inverseSineAn inverse sine curve.case sigmoidA sigmoid curve.case inverseSigmoidAn inverse sigmoid curve.case holdStartValueA curve that equals its start value for the entire duration.case jumpToEndValueA curve that equals its end value for the entire duration.

### PHASECurveType.jumpToEndValue | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecurvetype/jumptoendvalue

PHASE  PHASECurveType  PHASECurveType.jumpToEndValue CasePHASECurveType.jumpToEndValueA curve that equals its end value for the entire duration.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case jumpToEndValueDiscussionUse this type for step function curves, such as when mapping a continuously varying input value to a discrete set of output values.See AlsoTypescase linearA curve that increases uniformly with its input.case squaredA curve that increases at a rate that squares its input.case inverseSquaredA curve that increases at a rate of one divided by the input’s square.case cubedA curve that increases at a rate that cubes its input.case inverseCubedA curve that increases at a rate of one divided by the input’s cube.case sineA sine curve.case inverseSineAn inverse sine curve.case sigmoidA sigmoid curve.case inverseSigmoidAn inverse sigmoid curve.case holdStartValueA curve that equals its start value for the entire duration.

### PHASECurveType.linear | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecurvetype/linear

PHASE  PHASECurveType  PHASECurveType.linear CasePHASECurveType.linearA curve that increases uniformly with its input.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case linearDiscussionThe function y = x shapes this curve.See AlsoTypescase squaredA curve that increases at a rate that squares its input.case inverseSquaredA curve that increases at a rate of one divided by the input’s square.case cubedA curve that increases at a rate that cubes its input.case inverseCubedA curve that increases at a rate of one divided by the input’s cube.case sineA sine curve.case inverseSineAn inverse sine curve.case sigmoidA sigmoid curve.case inverseSigmoidAn inverse sigmoid curve.case holdStartValueA curve that equals its start value for the entire duration.case jumpToEndValueA curve that equals its end value for the entire duration.

### PHASECurveType.sigmoid | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecurvetype/sigmoid

PHASE  PHASECurveType  PHASECurveType.sigmoid CasePHASECurveType.sigmoidA sigmoid curve.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case sigmoidDiscussionAlso known as an s-curve, the sigmoid curve’s path movement is slow at either end and quick in the middle.See AlsoTypescase linearA curve that increases uniformly with its input.case squaredA curve that increases at a rate that squares its input.case inverseSquaredA curve that increases at a rate of one divided by the input’s square.case cubedA curve that increases at a rate that cubes its input.case inverseCubedA curve that increases at a rate of one divided by the input’s cube.case sineA sine curve.case inverseSineAn inverse sine curve.case inverseSigmoidAn inverse sigmoid curve.case holdStartValueA curve that equals its start value for the entire duration.case jumpToEndValueA curve that equals its end value for the entire duration.

### PHASECurveType.sine | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecurvetype/sine

PHASE  PHASECurveType  PHASECurveType.sine CasePHASECurveType.sineA sine curve.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case sineDiscussionThe function y = sin(x) shapes this curve. For a linear input along the x-axis, a sine curve gradually moves upward then downward in the y-direction, in a repeating fashion.See AlsoTypescase linearA curve that increases uniformly with its input.case squaredA curve that increases at a rate that squares its input.case inverseSquaredA curve that increases at a rate of one divided by the input’s square.case cubedA curve that increases at a rate that cubes its input.case inverseCubedA curve that increases at a rate of one divided by the input’s cube.case inverseSineAn inverse sine curve.case sigmoidA sigmoid curve.case inverseSigmoidAn inverse sigmoid curve.case holdStartValueA curve that equals its start value for the entire duration.case jumpToEndValueA curve that equals its end value for the entire duration.

### PHASECurveType.squared | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasecurvetype/squared

PHASE  PHASECurveType  PHASECurveType.squared CasePHASECurveType.squaredA curve that increases at a rate that squares its input.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case squaredDiscussionThe function y = x^2 shapes this curve.See AlsoTypescase linearA curve that increases uniformly with its input.case inverseSquaredA curve that increases at a rate of one divided by the input’s square.case cubedA curve that increases at a rate that cubes its input.case inverseCubedA curve that increases at a rate of one divided by the input’s cube.case sineA sine curve.case inverseSineAn inverse sine curve.case sigmoidA sigmoid curve.case inverseSigmoidAn inverse sigmoid curve.case holdStartValueA curve that equals its start value for the entire duration.case jumpToEndValueA curve that equals its end value for the entire duration.

## PHASEDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasedefinition

PHASE  PHASEDefinition ClassPHASEDefinitionA base class that adds a name to framework definitions.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEDefinitionOverviewVarious PHASE classes derive from this class, for example, PHASEMixerDefinition, PHASEMetaParameterDefinition, and PHASESoundEventNodeDefinition.This class represents a template from which PHASE creates concrete PHASEAsset subclasses at runtime. For example, when you register a global metaparameter definition using registerGlobalMetaParameter(metaParameterDefinition:), PHASE returns a PHASEAsset subclass, PHASEGlobalMetaParameterAsset, that identifies a usable metaparameter by name. To access the usable metaparameter, pass the PHASEGlobalMetaParameterAsset identifier into the globalMetaParameters dictionary.TopicsIdentifying a Definitionvar identifier: StringA unique name for the definition.RelationshipsInherits FromNSObjectInherited ByPHASEMetaParameterDefinitionPHASEMixerDefinitionPHASESoundEventNodeDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoAudio Layering and Effectsclass PHASEChannelMixerDefinitionAn audio-layering object that routes sound directly to the device’s output.class PHASEAmbientMixerDefinitionAn audio-layering object that outputs sound in a particular direction in 3D space.class PHASEMixerDefinitionAn object to initialize a mixer with a given configuration.class PHASEMixerAn object that combines multiple audio signals into a single signal.API ReferenceSpatial MixingDefine environmental characteristics that determine how sound plays in your app’s 3D soundscape.

### identifier | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasedefinition/identifier

PHASE  PHASEDefinition  identifier Instance PropertyidentifierA unique name for the definition.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var identifier: String { get }

## PHASEDirectivityModelParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasedirectivitymodelparameters

PHASE  PHASEDirectivityModelParameters ClassPHASEDirectivityModelParametersA base class for objects that direct sound.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEDirectivityModelParametersOverviewSeveral classes derive from this class that implement a unique strategy to direct sound. Rather than create an instance of this class, instantiate a subclass, such as PHASECardioidDirectivityModelParameters or PHASEConeDirectivityModelParameters.RelationshipsInherits FromNSObjectInherited ByPHASECardioidDirectivityModelParametersPHASEConeDirectivityModelParametersConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSound Directivityclass PHASECardioidDirectivityModelParametersAn object that directs sound in a heart-shaped curve surrounding a sound source.class PHASECardioidDirectivityModelSubbandParametersA data set that projects sound of a certain frequency outward in the shape of a heart.class PHASEConeDirectivityModelParametersAn object that directs sound in a cone-shaped curve that extends from a sound source.class PHASEConeDirectivityModelSubbandParametersA data set that projects sound of a certain frequency outward in the shape of a cone.

## PHASEDistanceModelFadeOutParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasedistancemodelfadeoutparameters

PHASE  PHASEDistanceModelFadeOutParameters ClassPHASEDistanceModelFadeOutParametersA distance over which the framework fades out sound.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEDistanceModelFadeOutParametersOverviewFor spatial sound output, the framework stops playing a sound when its distance from the listener surpases cullDistance. The framework gradually fades out the sound’s volume as the distance between the source and listener approaches cullDistance. Likewise, the framework gradually fades in the sound as the distance between the source and listener approaches 0. A PHASEDistanceModelParameters object provides an instance of this class to a spatial mixer; for more information, see fadeOutParameters.Specifying a Maximum Distance That Sound ReachesThe following code demonstrates a spatial mixer’s additional fade out. By setting fadeOutLength to 1.0, the framework begins to fade out a sound after its distance to the listener surpases 1.0.let fadeOut = PHASEDistanceModelFadeOutParameters(maximumDistance: 10.0,
 fadeOutLength: 1.0,
 curveType: PHASECurveType.linear)
piecewiseModel.fadeOutParameters = fadeOut
spatialMixer.distanceModelParameters = piecewiseModel
PHASEDistanceModelFadeOutParameters* fadeOut = 
    [[PHASEDistanceModelFadeOutParameters alloc] 
        initWithMaximumDistance:10.f 
        fadeOutLength:1.f curveType:PHASECurveTypeLinear];
piecewiseModel.fadeOutParameters = fadeOut;
spatialMixer.distanceModelParameters = piecewiseModel;
TopicsCreating the Distance Model Fade-Out Parametersinit(cullDistance: Double)Creates a distance beyond which sound sources stop playing.Inspecting the Cull Distancevar cullDistance: DoubleThe distance beyond which the framework doesn’t process the sound.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoDistance Modelingclass PHASEGeometricSpreadingDistanceModelParametersAn object that dissipates sound frequencies over distance.class PHASEEnvelopeDistanceModelParametersA graph of points and curves that shapes the volume of a sound over distance.class PHASEDistanceModelParametersA base class for a sound’s rate of change over distance.

### cullDistance | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasedistancemodelfadeoutparameters/culldistance

PHASE  PHASEDistanceModelFadeOutParameters  cullDistance Instance PropertycullDistanceThe distance beyond which the framework doesn’t process the sound.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var cullDistance: Double { get }DiscussionThe framework sets the value of this property to the init(cullDistance:) argument.

### init(cullDistance:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasedistancemodelfadeoutparameters/init(culldistance:)

PHASE  PHASEDistanceModelFadeOutParameters  init(cullDistance:) Initializerinit(cullDistance:)Creates a distance beyond which sound sources stop playing.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(cullDistance: Double) Parameters cullDistanceThe distance beyond which the framework doesn’t process a sound source. The value must be greater than or equal to 1.

## PHASEDistanceModelParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasedistancemodelparameters

PHASE  PHASEDistanceModelParameters ClassPHASEDistanceModelParametersA base class for a sound’s rate of change over distance.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEDistanceModelParametersOverviewWhen your app outputs sound with a 3D position and orientation, designate a subclass of this class to indicate the manner in which PHASE changes sound with distance. Assign an instance of either PHASEGeometricSpreadingDistanceModelParameters or PHASEEnvelopeDistanceModelParameters, depending on your app’s needs, to the PHASESpatialMixerDefinition class’s distanceModelParameters property.TopicsFading the Soundvar fadeOutParameters: PHASEDistanceModelFadeOutParameters?A distance over which the framework fades out the mixer’s sound.RelationshipsInherits FromNSObjectInherited ByPHASEEnvelopeDistanceModelParametersPHASEGeometricSpreadingDistanceModelParametersConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoDistance Modelingclass PHASEGeometricSpreadingDistanceModelParametersAn object that dissipates sound frequencies over distance.class PHASEEnvelopeDistanceModelParametersA graph of points and curves that shapes the volume of a sound over distance.class PHASEDistanceModelFadeOutParametersA distance over which the framework fades out sound.

### fadeOutParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasedistancemodelparameters/fadeoutparameters

PHASE  PHASEDistanceModelParameters  fadeOutParameters Instance PropertyfadeOutParametersA distance over which the framework fades out the mixer’s sound.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var fadeOutParameters: PHASEDistanceModelFadeOutParameters? { get set }DiscussionAs a sound source’s distance between the listener approaches the value of this property, the framework gradually lowers the sound’s volume to 0. Beyond this distance, PHASE culls the sound. This property offers an additional fade out that the framework applies on top of the spatial mixer’s distanceModelParameters.The framework calculates distance as the difference between the listener’s position and the sound-source position, scaled by the engine’s unitsPerMeter.

## PHASEDucker | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseducker

PHASE  PHASEDucker ClassPHASEDuckerAn object that manages competing sounds.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEDuckerOverviewWhen a sound plays in any of the source groups, this class lowers the volume of all the target groups so the listener hears the source sound more clearly. You set the source and target using PHASEGroup objects; see sourceGroups and targetGroups.Lower Background Music During a MonologueWhen an app plays a monologue, the background music may need to lower, or duck, to enhance the clarity of the vocals. The following code demonstrates a ducker that configures a group for background music, and another group for the vocals.let bgmGroup = PHASEGroup(identifier: "backgroundMusicGroup")
let voGroup = PHASEGroup(identifier: "voiceOverGroup")

let ducker = PHASEDucker(engine: myEngine, sourceGroups: [voGroup],
    targetGroups: [bgmGroup], gain: 0.25, attackTime: 0.25, releaseTime: 0.5,
    attackCurve: .linear, releaseCurve: .linear)

ducker.activate()
PHASEGroup* bgmGroup = [[PHASEGroup alloc] 
    initWithEngine:_objects->mEngine uid:@"backgroundMusicGroup"];
PHASEGroup* voGroup = [[PHASEGroup alloc] 
    initWithEngine:_objects->mEngine uid:@"voiceOverGroup"];

auto ducker = [[PHASEDucker alloc] 
    initWithEngine:_objects->mEngine
        sourceGroups:[NSSet setWithObject:voGroup]
        targetGroups:[NSSet setWithObject:bgmGroup]
        gain:0.25
        attackTime:0.25
        releaseTime:0.5
        attackCurve:PHASECurveTypeLinear
        releaseCurve:PHASECurveTypeLinear];

[ducker activate];
When an app sets up the ducking configuration in advance, PHASE automatically lowers the background music at runtime when the vocals play.TopicsCreating a Duckerinit(engine: PHASEEngine, sourceGroups: Set<PHASEGroup>, targetGroups: Set<PHASEGroup>, gain: Double, attackTime: Double, releaseTime: Double, attackCurve: PHASECurveType, releaseCurve: PHASECurveType)Creates an object that manages competing sounds.Specifying Soundsvar sourceGroups: Set<PHASEGroup>The sounds that determine volume reduction.var targetGroups: Set<PHASEGroup>The sounds that reduce in volume.Configuring Volume Reductionvar gain: DoubleThe amount of volume reduction.var identifier: StringA unique value for the ducker.var isActive: BoolA Boolean value that determines whether the ducker reduces sound.var attackTime: DoubleThe amount of time for sound reduction to reach maximum strength.var attackCurve: PHASECurveTypeA mathematical curve that shapes transition progress as sound reduction begins.var releaseTime: DoubleThe amount of time to transition from maximum sound reduction to no reduction.var releaseCurve: PHASECurveTypeA mathematical curve that shapes transition progress as sound reduction ends.Altering Soundfunc activate()Instructs the ducker to begin altering sound.func deactivate()Stops the ducker from altering sound.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSound Grouping and Managementclass PHASEGroupA container that shares audio parameters with a collection of sounds.class PHASEGroupPresetA collection of settings for groups.class PHASEGroupPresetSettingSettings for group presets.

### activate() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseducker/activate()

PHASE  PHASEDucker  activate() Instance Methodactivate()Instructs the ducker to begin altering sound.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func activate()See AlsoAltering Soundfunc deactivate()Stops the ducker from altering sound.

### attackCurve | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseducker/attackcurve

PHASE  PHASEDucker  attackCurve Instance PropertyattackCurveA mathematical curve that shapes transition progress as sound reduction begins.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var attackCurve: PHASECurveType { get }DiscussionThis mathematical curve shapes signal progress during the time it takes for sound reduction to reach maximum strength.See AlsoConfiguring Volume Reductionvar gain: DoubleThe amount of volume reduction.var identifier: StringA unique value for the ducker.var isActive: BoolA Boolean value that determines whether the ducker reduces sound.var attackTime: DoubleThe amount of time for sound reduction to reach maximum strength.var releaseTime: DoubleThe amount of time to transition from maximum sound reduction to no reduction.var releaseCurve: PHASECurveTypeA mathematical curve that shapes transition progress as sound reduction ends.

### attackTime | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseducker/attacktime

PHASE  PHASEDucker  attackTime Instance PropertyattackTimeThe amount of time for sound reduction to reach maximum strength.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var attackTime: Double { get }See AlsoConfiguring Volume Reductionvar gain: DoubleThe amount of volume reduction.var identifier: StringA unique value for the ducker.var isActive: BoolA Boolean value that determines whether the ducker reduces sound.var attackCurve: PHASECurveTypeA mathematical curve that shapes transition progress as sound reduction begins.var releaseTime: DoubleThe amount of time to transition from maximum sound reduction to no reduction.var releaseCurve: PHASECurveTypeA mathematical curve that shapes transition progress as sound reduction ends.

### deactivate() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseducker/deactivate()

PHASE  PHASEDucker  deactivate() Instance Methoddeactivate()Stops the ducker from altering sound.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func deactivate()See AlsoAltering Soundfunc activate()Instructs the ducker to begin altering sound.

### gain | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseducker/gain

PHASE  PHASEDucker  gain Instance PropertygainThe amount of volume reduction.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var gain: Double { get }DiscussionWhen source and target sounds play simultaneously, the value of this property determines the amount that the listener can hear the target sound.  A value of 0 results in full attenuation, and 1 results in no attenuation. The framework clamps the value to the range between 0 and 1.See AlsoConfiguring Volume Reductionvar identifier: StringA unique value for the ducker.var isActive: BoolA Boolean value that determines whether the ducker reduces sound.var attackTime: DoubleThe amount of time for sound reduction to reach maximum strength.var attackCurve: PHASECurveTypeA mathematical curve that shapes transition progress as sound reduction begins.var releaseTime: DoubleThe amount of time to transition from maximum sound reduction to no reduction.var releaseCurve: PHASECurveTypeA mathematical curve that shapes transition progress as sound reduction ends.

### identifier | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseducker/identifier

PHASE  PHASEDucker  identifier Instance PropertyidentifierA unique value for the ducker.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var identifier: String { get }See AlsoConfiguring Volume Reductionvar gain: DoubleThe amount of volume reduction.var isActive: BoolA Boolean value that determines whether the ducker reduces sound.var attackTime: DoubleThe amount of time for sound reduction to reach maximum strength.var attackCurve: PHASECurveTypeA mathematical curve that shapes transition progress as sound reduction begins.var releaseTime: DoubleThe amount of time to transition from maximum sound reduction to no reduction.var releaseCurve: PHASECurveTypeA mathematical curve that shapes transition progress as sound reduction ends.

### init(engine:sourceGroups:targetGroups:gain:attackTime:releaseTime:attackCurve:releaseCurve:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseducker/init(engine:sourcegroups:targetgroups:gain:attacktime:releasetime:attackcurve:releasecurve:)

PHASE  PHASEDucker  init(engine:sourceGroups:targetGroups:gain:attackTime:releaseTime:attackCurve:releaseCurve:) Initializerinit(engine:sourceGroups:targetGroups:gain:attackTime:releaseTime:attackCurve:releaseCurve:)Creates an object that manages competing sounds.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    engine: PHASEEngine,
    sourceGroups: Set<PHASEGroup>,
    targetGroups: Set<PHASEGroup>,
    gain: Double,
    attackTime: Double,
    releaseTime: Double,
    attackCurve: PHASECurveType,
    releaseCurve: PHASECurveType
) Parameters engineThe app’s instance of the framework object.sourceGroupsThe sounds that determine volume reduction.targetGroupsThe sounds that reduce in volume.gainThe volume level of the sound.attackTimeThe amount of time for sound reduction to reach maximum strength.releaseTimeThe amount of time to transition from maximum sound reduction to no reduction.attackCurveA mathematical curve that shapes transition progress during the time it takes to reach maximum sound reduction.releaseCurveA mathematical curve that shapes signal progress during the time it takes to transition from maximum sound reduction to no reduction.

### isActive | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseducker/isactive

PHASE  PHASEDucker  isActive Instance PropertyisActiveA Boolean value that determines whether the ducker reduces sound.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var isActive: Bool { get }See AlsoConfiguring Volume Reductionvar gain: DoubleThe amount of volume reduction.var identifier: StringA unique value for the ducker.var attackTime: DoubleThe amount of time for sound reduction to reach maximum strength.var attackCurve: PHASECurveTypeA mathematical curve that shapes transition progress as sound reduction begins.var releaseTime: DoubleThe amount of time to transition from maximum sound reduction to no reduction.var releaseCurve: PHASECurveTypeA mathematical curve that shapes transition progress as sound reduction ends.

### releaseCurve | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseducker/releasecurve

PHASE  PHASEDucker  releaseCurve Instance PropertyreleaseCurveA mathematical curve that shapes transition progress as sound reduction ends.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var releaseCurve: PHASECurveType { get }DiscussionThis mathematical curve shapes signal progress during the time it takes to transition from maximum sound reduction to no reduction.See AlsoConfiguring Volume Reductionvar gain: DoubleThe amount of volume reduction.var identifier: StringA unique value for the ducker.var isActive: BoolA Boolean value that determines whether the ducker reduces sound.var attackTime: DoubleThe amount of time for sound reduction to reach maximum strength.var attackCurve: PHASECurveTypeA mathematical curve that shapes transition progress as sound reduction begins.var releaseTime: DoubleThe amount of time to transition from maximum sound reduction to no reduction.

### releaseTime | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseducker/releasetime

PHASE  PHASEDucker  releaseTime Instance PropertyreleaseTimeThe amount of time to transition from maximum sound reduction to no reduction.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var releaseTime: Double { get }See AlsoConfiguring Volume Reductionvar gain: DoubleThe amount of volume reduction.var identifier: StringA unique value for the ducker.var isActive: BoolA Boolean value that determines whether the ducker reduces sound.var attackTime: DoubleThe amount of time for sound reduction to reach maximum strength.var attackCurve: PHASECurveTypeA mathematical curve that shapes transition progress as sound reduction begins.var releaseCurve: PHASECurveTypeA mathematical curve that shapes transition progress as sound reduction ends.

### sourceGroups | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseducker/sourcegroups

PHASE  PHASEDucker  sourceGroups Instance PropertysourceGroupsThe sounds that determine volume reduction.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var sourceGroups: Set<PHASEGroup> { get }See AlsoSpecifying Soundsvar targetGroups: Set<PHASEGroup>The sounds that reduce in volume.

### targetGroups | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseducker/targetgroups

PHASE  PHASEDucker  targetGroups Instance PropertytargetGroupsThe sounds that reduce in volume.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var targetGroups: Set<PHASEGroup> { get }See AlsoSpecifying Soundsvar sourceGroups: Set<PHASEGroup>The sounds that determine volume reduction.

## PHASEEngine | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine

PHASE  PHASEEngine ClassPHASEEngineAn object that manages audio assets, controls playback, and configures environmental effects.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEEngineOverviewBefore using PHASE, an app creates an instance of this object. Apps access all of the framework’s functionality through engine functions or properties, or through other PHASE classes into which you pass the engine object.Important You can create multiple engine instances, but normally, apps create only one.Create and Start the EngineTo create an engine object, choose a value for the init(updateMode:) argument that selects the desired control over scene setup and playback timing.// Apps that need precise audio synchronization and 
// synchronized dynamic mix control pass in `.manual`.
engine = PHASEEngine(updateMode: .automatic) 
Then, load your sound assets, sound event assets, and shapes for sound occlusion. Before your app attempts to play sounds, start the engine object.do { try engine.start() } 
catch { /* Handle the error. */ }
To stop audio playback and enable the engine to deallocate system resources, call the stop() function.engine.stop()
TopicsCreating an Engineinit(updateMode: PHASEEngine.UpdateMode)Creates an engine updated by the app or framework.init(updateMode: PHASEEngine.UpdateMode, renderingMode: PHASEEngine.RenderingMode)Creates a new engine that has both update and rendering modes.Betaenum UpdateModeModes that determine when the framework consumes API calls and updates internal state.enum RenderingModeModes that determine whether the system renders audio in process or out of process.BetaRegistering Audio Resourcesvar assetRegistry: PHASEAssetRegistryAn object that loads and unloads audio resources.Accessing Scene Hierarchyvar rootObject: PHASEObjectThe main object to which the app adds child objects.Defining Environmental Effectsvar defaultReverbPreset: PHASEReverbPresetThe environmental surroundings that determine how sound resonates.var defaultMedium: PHASEMediumThe physical matter through which sound travels.var outputSpatializationMode: PHASESpatializationModeThe mode the engine implements to create a 3D sound experience.Controlling and Inspecting Playback Statefunc pause()Pauses all audio playback.func start() throwsStarts or resumes all audio playback.func stop()Stops all audio playback.func update()Processes app commands and increments framework processing.var renderingState: PHASESoundEvent.RenderingStateThe status of the engine’s audio playback.var lastRenderTime: AVAudioTime?BetaManaging Groups of Soundsvar groups: [String : PHASEGroup]A list of named groups that contain sounds the app operates on collectively.var activeGroupPreset: PHASEGroupPreset?The settings that define playback for a group of sounds.var duckers: [PHASEDucker]An array of objects that reduce the volume of simultaneously playing sounds.Accessing In-Flight Audiovar soundEvents: [PHASESoundEvent]A collection of the sounds that play under various runtime circumstances.Measuring Unitsvar unitsPerMeter: DoubleA conversion factor from meters to your app’s preferred unit of measurement.var unitsPerSecond: DoubleA conversion factor from seconds to your app’s preferred unit of time.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSetupenum UpdateModeModes that determine when the framework consumes API calls and updates internal state.enum RenderingModeModes that determine whether the system renders audio in process or out of process.Betaclass PHASEAssetRegistryA central repository of audio assets.enum PHASENormalizationModeOptions that determine whether the framework adjusts a sound asset’s loudness for the user’s output device.enum PHASESpatializationModeThe manner in which PHASE outputs spatial audio.enum PHASEReverbPresetThe manner in which PHASE diffuses resonating sound.class PHASEMediumA property or quality of the environment that affects how sound travels.

### activeGroupPreset | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/activegrouppreset

PHASE  PHASEEngine  activeGroupPreset Instance PropertyactiveGroupPresetThe settings that define playback for a group of sounds.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var activeGroupPreset: PHASEGroupPreset? { get }DiscussionThis property returns the most recent group preset on which the app calls activate(). Group presets map a collection of sounds in a group to settings the app applies in a specific context. For more information, see PHASEGroupPreset.See AlsoManaging Groups of Soundsvar groups: [String : PHASEGroup]A list of named groups that contain sounds the app operates on collectively.var duckers: [PHASEDucker]An array of objects that reduce the volume of simultaneously playing sounds.

### assetRegistry | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/assetregistry

PHASE  PHASEEngine  assetRegistry Instance PropertyassetRegistryAn object that loads and unloads audio resources.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var assetRegistry: PHASEAssetRegistry { get }DiscussionThis property loads audio resources from disk to memory, and unloads audio resources to free up system resources.

### defaultMedium | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/defaultmedium

PHASE  PHASEEngine  defaultMedium Instance PropertydefaultMediumThe physical matter through which sound travels.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var defaultMedium: PHASEMedium { get set }See AlsoDefining Environmental Effectsvar defaultReverbPreset: PHASEReverbPresetThe environmental surroundings that determine how sound resonates.var outputSpatializationMode: PHASESpatializationModeThe mode the engine implements to create a 3D sound experience.

### defaultReverbPreset | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/defaultreverbpreset

PHASE  PHASEEngine  defaultReverbPreset Instance PropertydefaultReverbPresetThe environmental surroundings that determine how sound resonates.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var defaultReverbPreset: PHASEReverbPreset { get set }See AlsoDefining Environmental Effectsvar defaultMedium: PHASEMediumThe physical matter through which sound travels.var outputSpatializationMode: PHASESpatializationModeThe mode the engine implements to create a 3D sound experience.

### duckers | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/duckers

PHASE  PHASEEngine  duckers Instance PropertyduckersAn array of objects that reduce the volume of simultaneously playing sounds.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var duckers: [PHASEDucker] { get }See AlsoManaging Groups of Soundsvar groups: [String : PHASEGroup]A list of named groups that contain sounds the app operates on collectively.var activeGroupPreset: PHASEGroupPreset?The settings that define playback for a group of sounds.

### groups | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/groups

PHASE  PHASEEngine  groups Instance PropertygroupsA list of named groups that contain sounds the app operates on collectively.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var groups: [String : PHASEGroup] { get }See AlsoManaging Groups of Soundsvar activeGroupPreset: PHASEGroupPreset?The settings that define playback for a group of sounds.var duckers: [PHASEDucker]An array of objects that reduce the volume of simultaneously playing sounds.

### init(updateMode:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/init(updatemode:)

PHASE  PHASEEngine  init(updateMode:) Initializerinit(updateMode:)Creates an engine updated by the app or framework.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(updateMode: PHASEEngine.UpdateMode) Parameters updateModeAn option that controls the timing of internal framework updates.DiscussionThe argument you choose determines the rate at which the engine consumes user commands, performs internal updates, and executes callbacks.When an app calls a PHASE function, the framework defers processing the call until the next update. An engine you configure with PHASEEngine.UpdateMode.manual controls when the framework processes those calls. For example, an app can ensure that two sound events begin simultaneously by following their creation with an update(). Apps that don’t require advanced call synchronization select PHASEEngine.UpdateMode.automatic.See AlsoCreating an Engineinit(updateMode: PHASEEngine.UpdateMode, renderingMode: PHASEEngine.RenderingMode)Creates a new engine that has both update and rendering modes.Betaenum UpdateModeModes that determine when the framework consumes API calls and updates internal state.enum RenderingModeModes that determine whether the system renders audio in process or out of process.Beta

### init(updateMode:renderingMode:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/init(updatemode:renderingmode:)

PHASE  PHASEEngine  PHASEEngine  init(updateMode:renderingMode:) BetaInitializerinit(updateMode:renderingMode:)Creates a new engine that has both update and rendering modes.visionOS 26.0+Betainit(
    updateMode: PHASEEngine.UpdateMode,
    renderingMode: PHASEEngine.RenderingMode
) Parameters updateModeAn option that controls the timing of internal framework updates.renderingModeDefines where the engine applies rendering. See PHASEEngine.RenderingMode for more info.DiscussionIn this initializer, the updateMode argument behaves the same as it does for init(updateMode:). The renderingMode parameter value you choose determines where the system renders audio.An engine that you configure with PHASEEngine.RenderingMode.local renders audio locally, in process. Configuring an engine with PHASEEngine.RenderingMode.client renders audio remotely, in a secure rendering process.See AlsoCreating an Engineinit(updateMode: PHASEEngine.UpdateMode)Creates an engine updated by the app or framework.enum UpdateModeModes that determine when the framework consumes API calls and updates internal state.enum RenderingModeModes that determine whether the system renders audio in process or out of process.BetaBeta Software This documentation contains preliminary information about an API or technology in development. This information is subject to change, and software implemented according to this documentation should be tested with final operating system software.  Learn more about using Apple's beta software

### lastRenderTime | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/lastrendertime

PHASE  PHASEEngine  PHASEEngine  lastRenderTime BetaInstance PropertylastRenderTimeiOS 26.0+BetaiPadOS 26.0+BetaMac Catalyst 26.0+BetamacOS 26.0+BetatvOS 26.0+BetavisionOS 26.0+Betavar lastRenderTime: AVAudioTime? { get }DiscussionObtain the time for which the engine most recently rendered.Will return nil if the engine is not runningSee AlsoControlling and Inspecting Playback Statefunc pause()Pauses all audio playback.func start() throwsStarts or resumes all audio playback.func stop()Stops all audio playback.func update()Processes app commands and increments framework processing.var renderingState: PHASESoundEvent.RenderingStateThe status of the engine’s audio playback.Beta Software This documentation contains preliminary information about an API or technology in development. This information is subject to change, and software implemented according to this documentation should be tested with final operating system software.  Learn more about using Apple's beta software

### outputSpatializationMode | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/outputspatializationmode

PHASE  PHASEEngine  outputSpatializationMode Instance PropertyoutputSpatializationModeThe mode the engine implements to create a 3D sound experience.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var outputSpatializationMode: PHASESpatializationMode { get set }See AlsoDefining Environmental Effectsvar defaultReverbPreset: PHASEReverbPresetThe environmental surroundings that determine how sound resonates.var defaultMedium: PHASEMediumThe physical matter through which sound travels.

### pause() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/pause()

PHASE  PHASEEngine  pause() Instance Methodpause()Pauses all audio playback.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func pause()DiscussionTo resume paused playback, call start().See AlsoControlling and Inspecting Playback Statefunc start() throwsStarts or resumes all audio playback.func stop()Stops all audio playback.func update()Processes app commands and increments framework processing.var renderingState: PHASESoundEvent.RenderingStateThe status of the engine’s audio playback.var lastRenderTime: AVAudioTime?Beta

### PHASEEngine.RenderingMode | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/renderingmode

PHASE  PHASEEngine  PHASEEngine  PHASEEngine.RenderingMode BetaEnumerationPHASEEngine.RenderingModeModes that determine whether the system renders audio in process or out of process.visionOS 26.0+Betaenum RenderingModeOverviewTo define the manner in which PHASE renders audio content, select an option from this enumeration and pass it to the renderingMode parameter of the PHASEEngine initializer, init(updateMode:renderingMode:).TopicsModescase localA mode that indicates that the system renders audio in process.case clientA mode that instructs the system to render audio in a secure process.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoSetupclass PHASEEngineAn object that manages audio assets, controls playback, and configures environmental effects.enum UpdateModeModes that determine when the framework consumes API calls and updates internal state.class PHASEAssetRegistryA central repository of audio assets.enum PHASENormalizationModeOptions that determine whether the framework adjusts a sound asset’s loudness for the user’s output device.enum PHASESpatializationModeThe manner in which PHASE outputs spatial audio.enum PHASEReverbPresetThe manner in which PHASE diffuses resonating sound.class PHASEMediumA property or quality of the environment that affects how sound travels.Beta Software This documentation contains preliminary information about an API or technology in development. This information is subject to change, and software implemented according to this documentation should be tested with final operating system software.  Learn more about using Apple's beta software

#### PHASEEngine.RenderingMode.client | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/renderingmode/client

PHASE  PHASEEngine  PHASEEngine.RenderingMode  PHASEEngine  PHASEEngine.RenderingMode  PHASEEngine.RenderingMode.client BetaCasePHASEEngine.RenderingMode.clientA mode that instructs the system to render audio in a secure process.visionOS 26.0+Betacase clientDiscussionIn this mode, the engine is connected to an audio device and renders audio in real-time in a secure process. The engine receives inputs from the client and renders in a server. Updating an engine that has a client configuration syncs pending API commands with the server for processing.See AlsoModescase localA mode that indicates that the system renders audio in process.BetaBeta Software This documentation contains preliminary information about an API or technology in development. This information is subject to change, and software implemented according to this documentation should be tested with final operating system software.  Learn more about using Apple's beta software

#### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/renderingmode/init(rawvalue:)

PHASE  PHASEEngine  PHASEEngine.RenderingMode  PHASEEngine  PHASEEngine.RenderingMode  init(rawValue:) BetaInitializerinit(rawValue:)visionOS 26.0+Betainit?(rawValue: Int)Beta Software This documentation contains preliminary information about an API or technology in development. This information is subject to change, and software implemented according to this documentation should be tested with final operating system software.  Learn more about using Apple's beta software

#### PHASEEngine.RenderingMode.local | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/renderingmode/local

PHASE  PHASEEngine  PHASEEngine.RenderingMode  PHASEEngine  PHASEEngine.RenderingMode  PHASEEngine.RenderingMode.local BetaCasePHASEEngine.RenderingMode.localA mode that indicates that the system renders audio in process.visionOS 26.0+Betacase localDiscussionIn this mode, the engine is connected to an audio device and renders audio in real-time in the application process. The engine receives all of its inputs, for example, acoustic configuration, from the client. Updating an engine that has a local configuration executes any pending API commands locally.See AlsoModescase clientA mode that instructs the system to render audio in a secure process.BetaBeta Software This documentation contains preliminary information about an API or technology in development. This information is subject to change, and software implemented according to this documentation should be tested with final operating system software.  Learn more about using Apple's beta software

### renderingState | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/renderingstate

PHASE  PHASEEngine  renderingState Instance PropertyrenderingStateThe status of the engine’s audio playback.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var renderingState: PHASESoundEvent.RenderingState { get }DiscussionAccess this property to check the engine’s playback status. The value reflects the state that you control by calling one of the functions: start(), stop(), or pause().See AlsoControlling and Inspecting Playback Statefunc pause()Pauses all audio playback.func start() throwsStarts or resumes all audio playback.func stop()Stops all audio playback.func update()Processes app commands and increments framework processing.var lastRenderTime: AVAudioTime?Beta

### rootObject | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/rootobject

PHASE  PHASEEngine  rootObject Instance PropertyrootObjectThe main object to which the app adds child objects.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var rootObject: PHASEObject { get } Mentioned in  Playing sound from a location in a 3D scene DiscussionThe framework creates and sets the root object at engine instantiation.Avoid executing the following actions in your app; these actions cause the engine to generate a runtime error:Adding this object as a child.Altering the transform of this object.Copying this object.

### soundEvents | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/soundevents

PHASE  PHASEEngine  soundEvents Instance PropertysoundEventsA collection of the sounds that play under various runtime circumstances.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var soundEvents: [PHASESoundEvent] { get }

### start() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/start()

PHASE  PHASEEngine  start() Instance Methodstart()Starts or resumes all audio playback.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func start() throwsDiscussionThis function throws an error if the framework fails to start the engine.See AlsoControlling and Inspecting Playback Statefunc pause()Pauses all audio playback.func stop()Stops all audio playback.func update()Processes app commands and increments framework processing.var renderingState: PHASESoundEvent.RenderingStateThe status of the engine’s audio playback.var lastRenderTime: AVAudioTime?Beta

### stop() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/stop()

PHASE  PHASEEngine  stop() Instance Methodstop()Stops all audio playback.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func stop()See AlsoControlling and Inspecting Playback Statefunc pause()Pauses all audio playback.func start() throwsStarts or resumes all audio playback.func update()Processes app commands and increments framework processing.var renderingState: PHASESoundEvent.RenderingStateThe status of the engine’s audio playback.var lastRenderTime: AVAudioTime?Beta

### unitsPerMeter | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/unitspermeter

PHASE  PHASEEngine  unitsPerMeter Instance PropertyunitsPerMeterA conversion factor from meters to your app’s preferred unit of measurement.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var unitsPerMeter: Double { get set } Mentioned in  Playing sound from a location in a 3D scene DiscussionDistance-based properties throughout the framework apply the value you supply for this property to their value.See AlsoMeasuring Unitsvar unitsPerSecond: DoubleA conversion factor from seconds to your app’s preferred unit of time.

### unitsPerSecond | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/unitspersecond

PHASE  PHASEEngine  unitsPerSecond Instance PropertyunitsPerSecondA conversion factor from seconds to your app’s preferred unit of time.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var unitsPerSecond: Double { get set }DiscussionTime-based properties throughout the framework apply the value you supply for this property to their value.See AlsoMeasuring Unitsvar unitsPerMeter: DoubleA conversion factor from meters to your app’s preferred unit of measurement.

### update() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/update()

PHASE  PHASEEngine  update() Instance Methodupdate()Processes app commands and increments framework processing.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func update()DiscussionThis function consumes the app’s API calls since the last update(), adjusts internal systems, objects, increments parameters, and invokes the app’s queued callbacks. An API call may require several update() invocations before the output device reflects the call’s results.The framework ignores calls to this function for engines with updateMode set to PHASEEngine.UpdateMode.automatic; for more more information, see init(updateMode:).Note The frequency that the app calls this function doesn’t change the speed by which PHASE plays audio in real time.Update an Engine ManuallyOn an engine configured for manual updates (PHASEEngine.UpdateMode.manual), call this function periodically to instruct the framework to process API calls and perform internal updates. Call update() at a rate that matches your app’s visuals or logic update rate for optimal performance:Apps that process graphics at 60 FPS can invoke update() in their display link callback.Rates in the range of 240Hz to 30Hz offer equivalent audio performance, however apps that actively change the parameters of playing audio achieve smoother interpolation at a higher rate.If a game skips frames due to long running graphics routines, an app can throttle update() calls to values less than 30Hz without affecting audio quality as long as the system isn’t overloaded.This function offers thread safety for apps that intend to call update() off of the main thread.See AlsoControlling and Inspecting Playback Statefunc pause()Pauses all audio playback.func start() throwsStarts or resumes all audio playback.func stop()Stops all audio playback.var renderingState: PHASESoundEvent.RenderingStateThe status of the engine’s audio playback.var lastRenderTime: AVAudioTime?Beta

### PHASEEngine.UpdateMode | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/updatemode

PHASE  PHASEEngine  PHASEEngine.UpdateMode EnumerationPHASEEngine.UpdateModeModes that determine when the framework consumes API calls and updates internal state.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum UpdateModeOverviewTo define the manner in which PHASE processes commands and updates internal state, select an option from this enumeration and pass it to the updateMode parameter of the PHASEEngine initializer, init(updateMode:).TopicsModescase automaticA mode that indicates PHASE sets the timing of state adjustments.case manualA mode that indicates the app controls when the framework adjusts state.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoSetupclass PHASEEngineAn object that manages audio assets, controls playback, and configures environmental effects.enum RenderingModeModes that determine whether the system renders audio in process or out of process.Betaclass PHASEAssetRegistryA central repository of audio assets.enum PHASENormalizationModeOptions that determine whether the framework adjusts a sound asset’s loudness for the user’s output device.enum PHASESpatializationModeThe manner in which PHASE outputs spatial audio.enum PHASEReverbPresetThe manner in which PHASE diffuses resonating sound.class PHASEMediumA property or quality of the environment that affects how sound travels.

#### PHASEEngine.UpdateMode.automatic | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/updatemode/automatic

PHASE  PHASEEngine  PHASEEngine  PHASEEngine.UpdateMode  PHASEEngine.UpdateMode.automatic CasePHASEEngine.UpdateMode.automaticA mode that indicates PHASE sets the timing of state adjustments.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case automaticDiscussionIn this mode, the framework updates internal states at an optimized rate opaque to the app.See AlsoModescase manualA mode that indicates the app controls when the framework adjusts state.

#### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/updatemode/init(rawvalue:)

PHASE  PHASEEngine  PHASEEngine  PHASEEngine.UpdateMode  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

#### PHASEEngine.UpdateMode.manual | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseengine/updatemode/manual

PHASE  PHASEEngine  PHASEEngine  PHASEEngine.UpdateMode  PHASEEngine.UpdateMode.manual CasePHASEEngine.UpdateMode.manualA mode that indicates the app controls when the framework adjusts state.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case manualDiscussionIn this mode, the framework waits for the app to call update() before processing the app’s API calls and adjusting internal states.See AlsoModescase automaticA mode that indicates PHASE sets the timing of state adjustments.

## PHASEEnvelope | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseenvelope

PHASE  PHASEEnvelope ClassPHASEEnvelopeA collection of segments that connect to graph a complex curve over a linear input.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEEnvelopeOverviewIn traditional audio uses, an envelope defines a complex graph that determines the volume of audio data over an input duration. PHASE uses envelopes in a similar way. Given a value on the envelope’s input axis, the evaluate(x:) function plots and returns the result on the output axis. The following are possible uses of this class:Sound event nodes, such as PHASEBlendNodeDefinition, can shape their volume using an envelope; see addRange(envelope:subtree:).Distance models shape sounds with a 3D position using an envelope; see PHASEEnvelopeDistanceModelParameters.An envelope can do more than shape audio. To gradually change an envelope’s input value over time, use the PHASEMappedMetaParameterDefinition class, which creates a function with a metaparameter value as input. An app can use the numeric result for any purpose. For example, the x-axis can be distance and the y-axis can be playback rate.At runtime, PHASE determines whether a particular member of the segments array slopes up or down along the domain depending on the envelope’s particular use case.Create an Envelope and Shape its CurveTo use an envelope in your app, define its shape by defining a series of segments. Each segment specifies a curve that collectively connect to form a graph. The following code creates an envelope with a single segment that’s shaped like the lettter s:// Create a segments array.
var segments: [PHASEEnvelopeSegment] = []

// Create a single segment with a sigmoid curve to give "ease in, 
//  ease out" movement along the domain. Define an endpoint of (1, 1).
let segment = PHASEEnvelopeSegment(
    endPoint: simd_make_double2(1.0, 1.0), curveType: .sigmoid)

// Add the segment to the array.
segments.append(segment)

// Create the envelope and set the start point to (-1, -1).
let envelope = PHASEEnvelope(startPoint: simd_make_double2(-1.0, -1.0),
    segments: segments)
// Create a segments array.
NSMutableArray<PHASEEnvelopeSegment*>* segments = 
    [NSMutableArray new];

// Create a single segment with a sigmoid curve to give "ease in, 
//  ease out" movement along the domain. Define an endpoint of (1, 1).
PHASEEnvelopeSegment* segment = [[PHASEEnvelopeSegment alloc] 
    initWithEndPoint:simd_make_double2(1.0, 1.0) 
    curveType:PHASECurveTypeSigmoid];

// Add the segment to the array.
[segments addObject:segment];

// Create the envelope and set the start point to (-1, -1).
PHASEEnvelope* envelope = [[PHASEEnvelope alloc] 
    initWithStartPoint:simd_make_double2(-1.0, -1.0) 
    segments:segments];
The graph flexes at runtime depending on the source content on which the envelope operates. A PHASEEnvelope doesn’t constrain the evaluate(x:) function’s output to predertermined values. Instead, PHASE applies the envelope’s curves to the source content as a rate of change.TopicsCreating an Envelopeinit?(startPoint: simd_double2, segments: [PHASEEnvelopeSegment])Creates an envelope with a start point and segments.Inspecting the Envelopefunc evaluate(x: Double) -> DoubleProvides the height of the envelope for an input value.var segments: [PHASEEnvelopeSegment]An array of the envelope’s segments.var startPoint: simd_double2The starting point along the envelope’s duration.Bounding the Inputvar domain: PHASENumericPairThe range of the envelope’s possible input values.var range: PHASENumericPairThe bounds of the output value.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoDynamic Sound Controlclass PHASEEnvelopeSegmentA curved portion of an envelope.enum PHASECurveTypeOptions that apply a mathematical function to an input value.class PHASENumericPairAn ordered pair that defines a bounding box for an envelope.API ReferencePlayback ParameterizationChange the characteristics of in-flight audio by adjusting its properties at runtime.

### domain | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseenvelope/domain

PHASE  PHASEEnvelope  domain Instance PropertydomainThe range of the envelope’s possible input values.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var domain: PHASENumericPair { get }DiscussionThis property is an ordered pair that describes input values along the x axis for which the evaluate(x:) function can produce a non-zero output. The first number in the pair is the minimum input value, and the second number in the pair is the maximum input value.When an envelope graphs volume over time, the framework scales the domain by unitsPerSecond.  Likewise, when an envelope graphs volume over distance, the framework scales this property by unitsPerMeter.See AlsoBounding the Inputvar range: PHASENumericPairThe bounds of the output value.

### evaluate(x:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseenvelope/evaluate(x:)

PHASE  PHASEEnvelope  evaluate(x:) Instance Methodevaluate(x:)Provides the height of the envelope for an input value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func evaluate(x: Double) -> Double Parameters xA value within the envelope’s domain. The envelope clamps this parameter to a value within domain.Return ValueThe curve’s height for the argument x value.See AlsoInspecting the Envelopevar segments: [PHASEEnvelopeSegment]An array of the envelope’s segments.var startPoint: simd_double2The starting point along the envelope’s duration.

### init(startPoint:segments:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseenvelope/init(startpoint:segments:)

PHASE  PHASEEnvelope  init(startPoint:segments:) Initializerinit(startPoint:segments:)Creates an envelope with a start point and segments.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init?(
    startPoint: simd_double2,
    segments: [PHASEEnvelopeSegment]
) Parameters startPointThe start point of the envelope.segmentsAn array of segments.DiscussionFor an empty segments argument, the resulting envelope contains one segment where the end point matches the start point. If the segments argument contains more than one segment, the resulting segments array sorts in ascending order on the x value.Important The start point’s x value must be less than or equal to the segment with the lowest x value of all other segments, otherwise this function returns nil.

### range | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseenvelope/range

PHASE  PHASEEnvelope  range Instance PropertyrangeThe bounds of the output value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var range: PHASENumericPair { get }DiscussionThis property is an ordered pair that defines the range of possible output values along the y axis for the evaluate(x:) function. The first number in the pair is the minimum output value, and the second number in the pair is the maximum output value.See AlsoBounding the Inputvar domain: PHASENumericPairThe range of the envelope’s possible input values.

### segments | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseenvelope/segments

PHASE  PHASEEnvelope  segments Instance PropertysegmentsAn array of the envelope’s segments.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var segments: [PHASEEnvelopeSegment] { get }DiscussionThe framework sets the value of this property to the init(startPoint:segments:) argument.See AlsoInspecting the Envelopefunc evaluate(x: Double) -> DoubleProvides the height of the envelope for an input value.var startPoint: simd_double2The starting point along the envelope’s duration.

### startPoint | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseenvelope/startpoint

PHASE  PHASEEnvelope  startPoint Instance PropertystartPointThe starting point along the envelope’s duration.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var startPoint: simd_double2 { get }DiscussionThe framework sets the value of this property to the init(startPoint:segments:) argument.See AlsoInspecting the Envelopefunc evaluate(x: Double) -> DoubleProvides the height of the envelope for an input value.var segments: [PHASEEnvelopeSegment]An array of the envelope’s segments.

## PHASEEnvelopeDistanceModelParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseenvelopedistancemodelparameters

PHASE  PHASEEnvelopeDistanceModelParameters ClassPHASEEnvelopeDistanceModelParametersA graph of points and curves that shapes the volume of a sound over distance.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEEnvelopeDistanceModelParametersOverviewThis class provides an envelope that the app configures to dissipate the volume of a source’s sound with distance. The envelope describes a graph that the app configures using points and curves, where the input value is the distance between a sound source and the listener, and the output value is the sound’s volume.Dissipate Sound by Using an EnvelopeThe framework interprets this class’s envelope as a gain curve, which determines the sound’s volume over a distance. An envelope offers more precise control over sound dissipation than a geometric rolloffFactor. For example, the following code defines slow sound dissipation followed by a sharp decrease:var envelopeSegments : [PHASEEnvelopeSegment]!
envelopeSegments.append(PHASEEnvelopeSegment(endPoint: simd_make_double2(6.0, 1.0),
 curveType: PHASECurveType.sigmoid))
envelopeSegments.append(PHASEEnvelopeSegment(endPoint: simd_make_double2(9.0, 0.0),
 curveType:PHASECurveType.inverseCubed))
let distanceModelEnvelope = PHASEEnvelope(startPoint: simd_make_double2(0.0, 0.125),
 segments:envelopeSegments)

let piecewiseModel = PHASEEnvelopeDistanceModelParameters(envelope: distanceModelEnvelope!)

spatialMixer.distanceModelParameters = piecewiseModel
NSMutableArray<PHASEEnvelopeSegment*>* envelopeSegments = [NSMutableArray new];
[envelopeSegments addObject: [[PHASEEnvelopeSegment alloc] initWithEndPoint:simd_make_double2(6.0f, 1.0f) curveType:PHASECurveTypeSigmoid];
[envelopeSegments addObject: [[PHASEEnvelopeSegment alloc] initWithEndPoint:simd_make_double2(9.0f, 0.0f) curveType:PHASECurveTypeInverseCubed];
PHASEEnvelope* distanceModelEnvelope = [[PHASEEnvelope alloc] initWithStartPoint:simd_make_double2(0.0f, 0.125f) segments:envelopSegments];

PHASEEnvelopeDistanceModelParameters* piecewiseModel = [[PHASEEnvelopeDistanceModelParameters alloc] initWithEnvelope:distanceModelEnvelope];

spatialMixer.distanceModelParameters = piecewiseModel;
TopicsCreating the Distance Model Parametersinit(envelope: PHASEEnvelope)Creates the distance model parameters with an envelope.Shaping the Volume Over a Distancevar envelope: PHASEEnvelopeAn envelope that shapes sound dissipation over distance.RelationshipsInherits FromPHASEDistanceModelParametersConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoDistance Modelingclass PHASEGeometricSpreadingDistanceModelParametersAn object that dissipates sound frequencies over distance.class PHASEDistanceModelFadeOutParametersA distance over which the framework fades out sound.class PHASEDistanceModelParametersA base class for a sound’s rate of change over distance.

### envelope | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseenvelopedistancemodelparameters/envelope

PHASE  PHASEEnvelopeDistanceModelParameters  envelope Instance PropertyenvelopeAn envelope that shapes sound dissipation over distance.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var envelope: PHASEEnvelope { get }

### init(envelope:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseenvelopedistancemodelparameters/init(envelope:)

PHASE  PHASEEnvelopeDistanceModelParameters  init(envelope:) Initializerinit(envelope:)Creates the distance model parameters with an envelope.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(envelope: PHASEEnvelope) Parameters envelopeThe envelope that shapes sound dissipation over distance.

## PHASEEnvelopeSegment | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseenvelopesegment

PHASE  PHASEEnvelopeSegment ClassPHASEEnvelopeSegmentA curved portion of an envelope.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEEnvelopeSegmentOverviewThis class specifies a curve that determines the _y-_value rate of change over a particular portion of an envelope’s graph. For example, the difference between a PHASECurveType.cubed segment and an PHASECurveType.inverseCubed segment is that they share opposite rates of change; where the cubed curve’s y value changes fastest in the segment’s domain, the inverse-cubed curve changes slowest, and vice versa.TopicsCreating a Segmentinit(endPoint: simd_double2, curveType: PHASECurveType)Creates a curved portion of an envelope.Shaping a Segmentvar curveType: PHASECurveTypeA curve along the envelope that shapes the segment.var endPoint: simd_double2A point that identifies the end of the segment along the envelope.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoDynamic Sound Controlclass PHASEEnvelopeA collection of segments that connect to graph a complex curve over a linear input.enum PHASECurveTypeOptions that apply a mathematical function to an input value.class PHASENumericPairAn ordered pair that defines a bounding box for an envelope.API ReferencePlayback ParameterizationChange the characteristics of in-flight audio by adjusting its properties at runtime.

### curveType | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseenvelopesegment/curvetype

PHASE  PHASEEnvelopeSegment  curveType Instance PropertycurveTypeA curve along the envelope that shapes the segment.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var curveType: PHASECurveType { get set }DiscussionThe option you choose for this property determines the segment’s y_-_value rate of change along the input.See AlsoShaping a Segmentvar endPoint: simd_double2A point that identifies the end of the segment along the envelope.

### endPoint | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseenvelopesegment/endpoint

PHASE  PHASEEnvelopeSegment  endPoint Instance PropertyendPointA point that identifies the end of the segment along the envelope.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var endPoint: simd_double2 { get set }DiscussionThe framework connects this property to the prior segment’s end point, or the envelope startPoint, in the case of the first segment.See AlsoShaping a Segmentvar curveType: PHASECurveTypeA curve along the envelope that shapes the segment.

### init(endPoint:curveType:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseenvelopesegment/init(endpoint:curvetype:)

PHASE  PHASEEnvelopeSegment  init(endPoint:curveType:) Initializerinit(endPoint:curveType:)Creates a curved portion of an envelope.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    endPoint: simd_double2,
    curveType: PHASECurveType
) Parameters endPointThe segment’s end point.curveTypeA curve that defines the segment’s portion of the envelope.

## PHASEError | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseerror-swift.struct

PHASE  PHASEError StructurePHASEErrorAn error that PHASE reports.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+struct PHASEErrorTopicsIdentifying an Error Causestatic var initializeFailed: PHASEError.CodeAn error that indicates the engine failed to initialize.static var invalidObject: PHASEError.CodeAn error that indicates an object is invalid in a specific context.Creating an Errorenum CodeCodes that identify errors in PHASE.Type Propertiesstatic var errorDomain: StringRelationshipsConforms ToCustomNSErrorEquatableErrorHashableSendableSendableMetatypeSee AlsoFramework Errorsenum CodeCodes that identify errors in PHASE.let PHASEErrorDomain: StringA unique error domain for the framework.

### PHASEError.Code | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseerror-swift.struct/code

PHASE  PHASEError  PHASEError.Code EnumerationPHASEError.CodeCodes that identify errors in PHASE.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum CodeTopicsErrorscase initializeFailedAn error that indicates the engine failed to initialize.case invalidObjectAn error that indicates an object is invalid in a specific context.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoFramework Errorsstruct PHASEErrorAn error that PHASE reports.let PHASEErrorDomain: StringA unique error domain for the framework.

#### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseerror-swift.struct/code/init(rawvalue:)

PHASE  PHASEError  PHASEError  PHASEError.Code  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

#### PHASEError.Code.initializeFailed | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseerror-swift.struct/code/initializefailed

PHASE  PHASEError  PHASEError  PHASEError.Code  PHASEError.Code.initializeFailed CasePHASEError.Code.initializeFailedAn error that indicates the engine failed to initialize.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case initializeFailedSee AlsoErrorscase invalidObjectAn error that indicates an object is invalid in a specific context.

#### PHASEError.Code.invalidObject | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseerror-swift.struct/code/invalidobject

PHASE  PHASEError  PHASEError  PHASEError.Code  PHASEError.Code.invalidObject CasePHASEError.Code.invalidObjectAn error that indicates an object is invalid in a specific context.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case invalidObjectDiscussionThe addChild(_:) function throws this error if the specified child already has a parent in the scene graph hierarchy.See AlsoErrorscase initializeFailedAn error that indicates the engine failed to initialize.

### errorDomain | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseerror-swift.struct/errordomain

PHASE  PHASEError  errorDomain Type PropertyerrorDomainiOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var errorDomain: String { get }

### initializeFailed | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseerror-swift.struct/initializefailed

PHASE  PHASEError  initializeFailed Type PropertyinitializeFailedAn error that indicates the engine failed to initialize.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var initializeFailed: PHASEError.Code { get }See AlsoIdentifying an Error Causestatic var invalidObject: PHASEError.CodeAn error that indicates an object is invalid in a specific context.

### invalidObject | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseerror-swift.struct/invalidobject

PHASE  PHASEError  invalidObject Type PropertyinvalidObjectAn error that indicates an object is invalid in a specific context.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var invalidObject: PHASEError.Code { get }DiscussionThe addChild(_:) function throws this error if the specified child already has a parent in the scene graph hierarchy.See AlsoIdentifying an Error Causestatic var initializeFailed: PHASEError.CodeAn error that indicates the engine failed to initialize.

## PHASEErrorDomain | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseerrordomain

PHASE  PHASEErrorDomain Global VariablePHASEErrorDomainA unique error domain for the framework.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+let PHASEErrorDomain: StringDiscussionFor more information on Core Foundation error domains, see Error domains.See AlsoFramework Errorsstruct PHASEErrorAn error that PHASE reports.enum CodeCodes that identify errors in PHASE.

## PHASEGeneratorNodeDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegeneratornodedefinition

PHASE  PHASEGeneratorNodeDefinition ClassPHASEGeneratorNodeDefinitionA base class for nodes that provide audio data to generate sound.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEGeneratorNodeDefinitionOverviewThis class encapsulates shared logic for subclasses that provide audio data to a mixer for sound output, namely PHASESamplerNodeDefinition and PHASEPushStreamNodeDefinition.TopicsCalibrating Loudnessfunc setCalibrationMode(calibrationMode: PHASECalibrationMode, level: Double)Selects a loudness correction strategy and reference level.var calibrationMode: PHASECalibrationModeA sound pressure level strategy for loudness correction.var level: DoubleThe node’s loudness.Defining an Output Strategyvar mixerDefinition: PHASEMixerDefinitionAn object that combines audio layers for the node’s output.Joining a Groupvar group: PHASEGroup?A group this node conforms to for gain and rate control.Controlling Audio Playbackvar rate: DoubleA playback speed for the node’s audio.var rateMetaParameterDefinition: PHASENumberMetaParameterDefinition?A meta parameter that dynamically changes the audio’s rate.var gainMetaParameterDefinition: PHASENumberMetaParameterDefinition?A meta parameter that dynamically changes the audio’s loudness.RelationshipsInherits FromPHASESoundEventNodeDefinitionInherited ByPHASEPullStreamNodeDefinitionPHASEPushStreamNodeDefinitionPHASESamplerNodeDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoAudio-Providing Nodesclass PHASESamplerNodeDefinitionA node that plays complete audio data.enum PHASEPlaybackModeLoop options for audio playback.class PHASEPushStreamNodeDefinitionA node that plays a sequence of audio buffers.class PHASEPushStreamNodeAn audio stream you manage to provide a sound buffer data.struct PHASEPushStreamBufferOptionsOptions that inform PHASE of an audio-stream buffer’s playback priority.enum PHASECalibrationModeCalibration options for sound pressure level.

### calibrationMode | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegeneratornodedefinition/calibrationmode

PHASE  PHASEGeneratorNodeDefinition  calibrationMode Instance PropertycalibrationModeA sound pressure level strategy for loudness correction.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var calibrationMode: PHASECalibrationMode { get }DiscussionThe default value is PHASECalibrationMode.none. To set a value, call setCalibrationMode(calibrationMode:level:).See AlsoCalibrating Loudnessfunc setCalibrationMode(calibrationMode: PHASECalibrationMode, level: Double)Selects a loudness correction strategy and reference level.var level: DoubleThe node’s loudness.

### gainMetaParameterDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegeneratornodedefinition/gainmetaparameterdefinition

PHASE  PHASEGeneratorNodeDefinition  gainMetaParameterDefinition Instance PropertygainMetaParameterDefinitionA meta parameter that dynamically changes the audio’s loudness.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var gainMetaParameterDefinition: PHASENumberMetaParameterDefinition? { get set }See AlsoControlling Audio Playbackvar rate: DoubleA playback speed for the node’s audio.var rateMetaParameterDefinition: PHASENumberMetaParameterDefinition?A meta parameter that dynamically changes the audio’s rate.

### group | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegeneratornodedefinition/group

PHASE  PHASEGeneratorNodeDefinition  group Instance PropertygroupA group this node conforms to for gain and rate control.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+weak var group: PHASEGroup? { get set }Discussion

### level | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegeneratornodedefinition/level

PHASE  PHASEGeneratorNodeDefinition  level Instance PropertylevelThe node’s loudness.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var level: Double { get }DiscussionThe default value is 1. To set a value, call setCalibrationMode(calibrationMode:level:).See AlsoCalibrating Loudnessfunc setCalibrationMode(calibrationMode: PHASECalibrationMode, level: Double)Selects a loudness correction strategy and reference level.var calibrationMode: PHASECalibrationModeA sound pressure level strategy for loudness correction.

### mixerDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegeneratornodedefinition/mixerdefinition

PHASE  PHASEGeneratorNodeDefinition  mixerDefinition Instance PropertymixerDefinitionAn object that combines audio layers for the node’s output.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var mixerDefinition: PHASEMixerDefinition { get }

### rate | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegeneratornodedefinition/rate

PHASE  PHASEGeneratorNodeDefinition  rate Instance PropertyrateA playback speed for the node’s audio.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var rate: Double { get set }DiscussionThe value clamps to the range [0.25, 4]. The default value is 1, which doesn’t change the source audio’s rate. Values higher than 1 speed up playback, and lower values slow it down.See AlsoControlling Audio Playbackvar rateMetaParameterDefinition: PHASENumberMetaParameterDefinition?A meta parameter that dynamically changes the audio’s rate.var gainMetaParameterDefinition: PHASENumberMetaParameterDefinition?A meta parameter that dynamically changes the audio’s loudness.

### rateMetaParameterDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegeneratornodedefinition/ratemetaparameterdefinition

PHASE  PHASEGeneratorNodeDefinition  rateMetaParameterDefinition Instance PropertyrateMetaParameterDefinitionA meta parameter that dynamically changes the audio’s rate.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var rateMetaParameterDefinition: PHASENumberMetaParameterDefinition? { get set }See AlsoControlling Audio Playbackvar rate: DoubleA playback speed for the node’s audio.var gainMetaParameterDefinition: PHASENumberMetaParameterDefinition?A meta parameter that dynamically changes the audio’s loudness.

### setCalibrationMode(calibrationMode:level:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegeneratornodedefinition/setcalibrationmode(calibrationmode:level:)

PHASE  PHASEGeneratorNodeDefinition  setCalibrationMode(calibrationMode:level:) Instance MethodsetCalibrationMode(calibrationMode:level:)Selects a loudness correction strategy and reference level.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func setCalibrationMode(
    calibrationMode: PHASECalibrationMode,
    level: Double
) Parameters calibrationModeA given strategy for sound pressure level. For a consistent user experience across platforms and output devices, choose PHASECalibrationMode.absoluteSpl or PHASECalibrationMode.relativeSpl.levelThe loudness. The calibration mode determines this value’s unit and range.See AlsoCalibrating Loudnessvar calibrationMode: PHASECalibrationModeA sound pressure level strategy for loudness correction.var level: DoubleThe node’s loudness.

## PHASEGeometricSpreadingDistanceModelParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegeometricspreadingdistancemodelparameters

PHASE  PHASEGeometricSpreadingDistanceModelParameters ClassPHASEGeometricSpreadingDistanceModelParametersAn object that dissipates sound frequencies over distance.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEGeometricSpreadingDistanceModelParameters Mentioned in  Playing sound from a location in a 3D scene OverviewThis class implements a roll-off effect — a strategy that aims to model the real-world manner in which sound changes with distance. When the distance between a sound and listener changes, the roll-off effect dissipates certain audio frequencies more than others.Dissipate Sound by Choosing a Roll-Off FactorPHASE emphasizes or deemphasizes the volume loss of the mixer’s sound sources based on the rolloffFactor you choose. For example, a rolloffFactor of 1.0 reduces sound between the source and listener by 6 dB for every doubling of distance. At 2.0, the loss doubles. At 0.5, the loss halves.To add a geometric-spreading distance model to a spatial sounds, set the mixer’s distanceModelParameters property to an instance of this class. For example:let simpleModel = PHASEGeometricSpreadingDistanceModelParameters()
simpleModel.rolloffFactor = 1.0
spatialMixer.distanceModelParameters = simpleModel
PHASEGeometricSpreadingDistanceModelParameters* simpleModel = [[PHASEGeometricSpreadingDistanceModelParameters alloc] init];
simpleModel.rolloffFactor = 1.f;
spatialMixer.distanceModelParameters = simpleModel;
TopicsCreating the Distance Model Parametersinit()Creates the geometric spreading distance model parameters.Setting the Roll-Off Factorvar rolloffFactor: DoubleA value that fades specific frequencies over a distance.RelationshipsInherits FromPHASEDistanceModelParametersConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoDistance Modelingclass PHASEEnvelopeDistanceModelParametersA graph of points and curves that shapes the volume of a sound over distance.class PHASEDistanceModelFadeOutParametersA distance over which the framework fades out sound.class PHASEDistanceModelParametersA base class for a sound’s rate of change over distance.

### init() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegeometricspreadingdistancemodelparameters/init()

PHASE  PHASEGeometricSpreadingDistanceModelParameters  init() Initializerinit()Creates the geometric spreading distance model parameters.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init()

### rolloffFactor | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegeometricspreadingdistancemodelparameters/rollofffactor

PHASE  PHASEGeometricSpreadingDistanceModelParameters  rolloffFactor Instance PropertyrolloffFactorA value that fades specific frequencies over a distance.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var rolloffFactor: Double { get set } Mentioned in  Playing sound from a location in a 3D scene DiscussionThe framework clamps a value to the range [0.0, greatestFiniteMagnitude].A roll-off effect changes the frequencies of a sound as it dissipates with distance. A value of 0.0 disables the roll-off effect. A value of 0.5 havles the roll-off. The default value is 1.0, which produces a realistic roll-off effect. A value of 2.0 amplifies the roll-off effect.

## PHASEGlobalMetaParameterAsset | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseglobalmetaparameterasset

PHASE  PHASEGlobalMetaParameterAsset ClassPHASEGlobalMetaParameterAssetA reference to a registered metaparameter that the app can share with multiple sound events or sources.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEGlobalMetaParameterAssetOverviewThe engine’s registerGlobalMetaParameter(metaParameterDefinition:) function returns an instance of this class for a parameter you register. Then, you access the actual metaparameter by using this class’s identifier as the key for metaparameter dictionary, for example, a sound event’s metaParameters or the asset registry’s globalMetaParameters.As an opaque derived object, this class adds no properties to the subclass.RelationshipsInherits FromPHASEAssetConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoBase Metaparametersclass PHASEMetaParameterA named parameter with a value that the app can change over time.class PHASEMetaParameterDefinitionA specification for a named parameter with a constant value.

## PHASEGroup | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegroup

PHASE  PHASEGroup ClassPHASEGroupA container that shares audio parameters with a collection of sounds.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEGroupOverviewWith all the sounds it contains, a group shares settings like gain, playback rate, mute, and solo. Groups are nonhierarchical and don’t overlap — that is, each sound event associates with only one group.Apply Group Settings to SoundsYou can apply settings to the sounds a group contains. For instance, an app can share volume settings with various sound effects and dialogue audio groups. The following example creates a group for background audio, such as environmental sound layers played with ambient music. By interpolating the group’s gain setting, the audio fade applies to every sound in the group.// Allocate an engine and stereo mixer.
let stereoLayout = AVAudioChannelLayout(layoutTag: kAudioChannelLayoutTag_Stereo)!
let myEngine = PHASEEngine(updateMode: .automatic)
let stereoMixer = PHASEChannelMixerDefinition(channelLayout:stereoLayout)

// Create a group object.
let bgmGroup = PHASEGroup(identifier:"backgroundMusicGroup")
bgmGroup.register(engine: myEngine)

// Create a sound event node definition for background music.
let backgroundMusicSampler = PHASESamplerNodeDefinition(soundAssetIdentifier: "backgroundMusic", mixerDefinition: stereoMixer)
        
// Add the sound node to the group.
backgroundMusicSampler.group = myEngine.groups["backgroundMusicGroup"]
        
// Set group gain to zero.
bgmGroup.gain = 0
        
// Create a sound event to play the music.
var bgmEvent: PHASESoundEvent?
do {
    try bgmEvent = PHASESoundEvent(engine: myEngine, assetIdentifier: "backgroundMusicEventAsset")
} catch {
    fatalError("Error occurred: \(error.localizedDescription)")
}
        
// Queue the background music to play.
bgmEvent?.start() { reason in
    print("Started. Status: \(reason)")
}
        
// Fade in the music over two seconds.
bgmGroup.fadeGain(gain: 1.0, duration: 2.0, curveType: .linear)
// Create a group object.
PHASEGroup* bgmGroup = [[PHASEGroup alloc] initWithEngine:myEngine uid@"backgroundMusicGroup"];

// Create a sound event node definition for background music. 
PHASESamplerNodeDefinition* backgroundMusicSampler = [[PHASESamplerNodeDefinition alloc] initWithSoundAssetUID:@"backgroundMusic" mixerDefinition:mixer];

// Add the sound node to the group.
backgroundMusicSampler.group = myPHASEEngine.activeGroups[@"backgroundMusicGroup"];

// Set group gain to zero. 
bgmGroup.gain = 0;

// Create a sound event to play the music.
PHASESoundEvent* bgmEvent = [[PHASESoundEvent alloc] initWithEngine:_objects->mEngine
    registeredSoundEventNodeAssetUID:@"backgroundMusicEventAsset" outError:nil];

// Queue the background music to play.
NSError* myError = nil;
[bgmEvent startAndReturnError:&myError];
 
// Fade in the music over two seconds.
[bgmGroup fadeGain:1.0 duration:2.0 curveType:PHASECurveTypeLinear];
TopicsCreating a Groupinit(identifier: String)Creates a group with a unique name.Identifying the Groupvar identifier: StringA unique name for the group.Defining the Groupfunc register(engine: PHASEEngine)Adds the group to the engine’s dictionary.func unregisterFromEngine()Removes the group from the engine’s dictionary.Conrolling Loudnessvar gain: DoubleModifies the volume of the group’s sounds.func fadeGain(gain: Double, duration: Double, curveType: PHASECurveType)Adjusts the volume of the sounds in a group gradually.Adjusting Playback Speedvar rate: DoubleThe group’s playback speed.func fadeRate(rate: Double, duration: Double, curveType: PHASECurveType)Adjusts the playback speed of the sounds in a group gradually.Silencing Soundsfunc mute()Silences the group.func unmute()Restores the group’s volume.var isMuted: BoolA Boolean value that indicates whether the app silences the group.func solo()Silences all other groups.func unsolo()Restores the other groups’ volume.var isSoloed: BoolA Boolean value that indicates whether the app silences all groups other than this group.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSound Grouping and Managementclass PHASEGroupPresetA collection of settings for groups.class PHASEGroupPresetSettingSettings for group presets.class PHASEDuckerAn object that manages competing sounds.

### fadeGain(gain:duration:curveType:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegroup/fadegain(gain:duration:curvetype:)

PHASE  PHASEGroup  fadeGain(gain:duration:curveType:) Instance MethodfadeGain(gain:duration:curveType:)Adjusts the volume of the sounds in a group gradually.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func fadeGain(
    gain: Double,
    duration: Double,
    curveType: PHASECurveType
) Parameters gainThe target volume.durationThe total time to complete the volume adjustment. The framework scales this value by unitsPerSecond.curveTypeA selection that specifies a mathematical curve that shapes the volume adjustment over time.See AlsoConrolling Loudnessvar gain: DoubleModifies the volume of the group’s sounds.

### fadeRate(rate:duration:curveType:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegroup/faderate(rate:duration:curvetype:)

PHASE  PHASEGroup  fadeRate(rate:duration:curveType:) Instance MethodfadeRate(rate:duration:curveType:)Adjusts the playback speed of the sounds in a group gradually.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func fadeRate(
    rate: Double,
    duration: Double,
    curveType: PHASECurveType
) Parameters rateThe target playback speed.durationThe total time to adjust the playback speed. The framework scales this value by unitsPerSecond.curveTypeA selection that specifies a mathematical curve that shapes the playback speed adjustment over time.See AlsoAdjusting Playback Speedvar rate: DoubleThe group’s playback speed.

### gain | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegroup/gain

PHASE  PHASEGroup  gain Instance PropertygainModifies the volume of the group’s sounds.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var gain: Double { get set }DiscussionThis property modifies the volume of all audio in the group. The framework clamps the value to the range between 0 and 1, where 0 silences the audio and 1 doesn’t modify the original volume.See AlsoConrolling Loudnessfunc fadeGain(gain: Double, duration: Double, curveType: PHASECurveType)Adjusts the volume of the sounds in a group gradually.

### identifier | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegroup/identifier

PHASE  PHASEGroup  identifier Instance PropertyidentifierA unique name for the group.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var identifier: String { get }

### init(identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegroup/init(identifier:)

PHASE  PHASEGroup  init(identifier:) Initializerinit(identifier:)Creates a group with a unique name.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(identifier: String) Parameters identifierA unique name for the group.

### isMuted | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegroup/ismuted

PHASE  PHASEGroup  isMuted Instance PropertyisMutedA Boolean value that indicates whether the app silences the group.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var isMuted: Bool { get }See AlsoSilencing Soundsfunc mute()Silences the group.func unmute()Restores the group’s volume.func solo()Silences all other groups.func unsolo()Restores the other groups’ volume.var isSoloed: BoolA Boolean value that indicates whether the app silences all groups other than this group.

### isSoloed | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegroup/issoloed

PHASE  PHASEGroup  isSoloed Instance PropertyisSoloedA Boolean value that indicates whether the app silences all groups other than this group.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var isSoloed: Bool { get }See AlsoSilencing Soundsfunc mute()Silences the group.func unmute()Restores the group’s volume.var isMuted: BoolA Boolean value that indicates whether the app silences the group.func solo()Silences all other groups.func unsolo()Restores the other groups’ volume.

### mute() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegroup/mute()

PHASE  PHASEGroup  mute() Instance Methodmute()Silences the group.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func mute()See AlsoSilencing Soundsfunc unmute()Restores the group’s volume.var isMuted: BoolA Boolean value that indicates whether the app silences the group.func solo()Silences all other groups.func unsolo()Restores the other groups’ volume.var isSoloed: BoolA Boolean value that indicates whether the app silences all groups other than this group.

### rate | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegroup/rate

PHASE  PHASEGroup  rate Instance PropertyrateThe group’s playback speed.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var rate: Double { get set }See AlsoAdjusting Playback Speedfunc fadeRate(rate: Double, duration: Double, curveType: PHASECurveType)Adjusts the playback speed of the sounds in a group gradually.

### register(engine:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegroup/register(engine:)

PHASE  PHASEGroup  register(engine:) Instance Methodregister(engine:)Adds the group to the engine’s dictionary.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func register(engine: PHASEEngine) Parameters engineThe engine with which to register this group.DiscussionThe function generates an exception if the argument is nil or if engine already contains the group. For more information, see groups.See AlsoDefining the Groupfunc unregisterFromEngine()Removes the group from the engine’s dictionary.

### solo() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegroup/solo()

PHASE  PHASEGroup  solo() Instance Methodsolo()Silences all other groups.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func solo()DiscussionThe engine silences all groups other than the group on which the app calls this function.See AlsoSilencing Soundsfunc mute()Silences the group.func unmute()Restores the group’s volume.var isMuted: BoolA Boolean value that indicates whether the app silences the group.func unsolo()Restores the other groups’ volume.var isSoloed: BoolA Boolean value that indicates whether the app silences all groups other than this group.

### unmute() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegroup/unmute()

PHASE  PHASEGroup  unmute() Instance Methodunmute()Restores the group’s volume.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func unmute()See AlsoSilencing Soundsfunc mute()Silences the group.var isMuted: BoolA Boolean value that indicates whether the app silences the group.func solo()Silences all other groups.func unsolo()Restores the other groups’ volume.var isSoloed: BoolA Boolean value that indicates whether the app silences all groups other than this group.

### unregisterFromEngine() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegroup/unregisterfromengine()

PHASE  PHASEGroup  unregisterFromEngine() Instance MethodunregisterFromEngine()Removes the group from the engine’s dictionary.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func unregisterFromEngine()DiscussionFor more information, see groups.See AlsoDefining the Groupfunc register(engine: PHASEEngine)Adds the group to the engine’s dictionary.

### unsolo() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegroup/unsolo()

PHASE  PHASEGroup  unsolo() Instance Methodunsolo()Restores the other groups’ volume.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func unsolo()See AlsoSilencing Soundsfunc mute()Silences the group.func unmute()Restores the group’s volume.var isMuted: BoolA Boolean value that indicates whether the app silences the group.func solo()Silences all other groups.var isSoloed: BoolA Boolean value that indicates whether the app silences all groups other than this group.

## PHASEGroupPreset | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegrouppreset

PHASE  PHASEGroupPreset ClassPHASEGroupPresetA collection of settings for groups.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEGroupPresetOverviewGroup presets pair groups with audio settings that your app can apply to specific sounds at a particular time in your app’s life cycle. This class enables many predefined group settings to take effect all at once.Toggle Between Group PresetsThe group preset’s utility materializes when you switch between settings. The following example creates two group presets: one for an in-game experience and another for a menu that displays when the user pauses the app.// Create sound group objects.
let bgmGroup = PHASEGroup(identifier:"backgroundMusicGroup")
let voGroup = PHASEGroup(identifier:"voiceOverGroup")
let menuGroup = PHASEGroup(identifier:"menuSoundsGroup")

// Register the groups with the engine.
bgmGroup.register(engine: myEngine)
voGroup.register(engine: myEngine)
menuGroup.register(engine: myEngine)
        
// Create settings for the groups.
let groupSettingFullVolume = PHASEGroupPresetSetting(gain: 1.0, rate: 1.0, gainCurveType: .linear, rateCurveType: .linear)
let groupSettingZeroVolume = PHASEGroupPresetSetting(gain: 0.0, rate: 1.0, gainCurveType: .linear, rateCurveType: .linear)
        
// Create a dictionary for the `settings` argument of the group preset initializer.
var pauseMenuDictionary: [String : PHASEGroupPresetSetting] = [:]
        
// Enable volume only for menu group sounds.
pauseMenuDictionary[menuGroup.identifier] = groupSettingFullVolume
pauseMenuDictionary[bgmGroup.identifier] = groupSettingZeroVolume
pauseMenuDictionary[voGroup.identifier] = groupSettingZeroVolume
let pauseMenuPreset = PHASEGroupPreset(engine: myEngine, settings: pauseMenuDictionary, timeToTarget: 1.0, timeToReset: 1.0)
        
// Create a settings dictionary for the in-game experience.
var inGameDictionary: [String : PHASEGroupPresetSetting] = [:]

// Enable volume only for in-game sounds.
inGameDictionary[menuGroup.identifier] = groupSettingZeroVolume
inGameDictionary[bgmGroup.identifier] = groupSettingFullVolume
inGameDictionary[voGroup.identifier] = groupSettingFullVolume
let inGamePreset = PHASEGroupPreset(engine: myEngine, settings: inGameDictionary, timeToTarget: 1.0, timeToReset: 1.0)
        
// Activate the pause menu preset when the user pauses the app.
pauseMenuPreset.activate()

// Activate the in-game preset when the user resumes the app.
inGamePreset.activate()

// Clear the current preset by deactivating it.
if let groupPreset = myEngine.activeGroupPreset {
    groupPreset.deactivate()
}
// Create groups for the sounds. 
PHASEGroup* bgmGroup = [[PHASEGroup alloc] initWithEngine:_objects->mEngine uid:@"backgroundMusicGroup"];
PHASEGroup* voGroup = [[PHASEGroup alloc] initWithEngine:_objects->mEngine uid:@"voiceOverGroup"];
PHASEGroup* menuGroup = [[PHASEGroup alloc] initWithEngine:_objects->mEngine uid:@"menuSoundsGroup"];

// Create settings for the groups.
PHASEGroupPresetSetting* groupSettingFullVolume = [PHASEGroupPresetSetting alloc] initWithGain:1
    rate:1 gainCurveType:PHASECurveTypeLinear rateCurveType:PHASECurveTypeLinear];
                                                
PHASEGroupPresetSetting* groupSettingZeroVolume = [PHASEGroupPresetSetting alloc] initWithGain:0
    rate:1 gainCurveType:PHASECurveTypeLinear rateCurveType:PHASECurveTypeLinear];

// Create a dictionary for the `settings` argument of the group preset initializer.
NSMutableDictionary<PHASEGroup*, PHASEGroupPresetSetting*> pauseMenuDictionary;

// Enable volume only for menu group sounds.
[pauseMenuDictionary setObject:groupSettingFullVolume forKey:menuGroup]
[pauseMenuDictionary setObject:groupSettingZeroVolume forKey:bgmGroup]
[pauseMenuDictionary setObject:groupSettingZeroVolume forKey:voGroup]
PHASEGroupPreset* pauseMenuPreset = [[PHASEGroupPreset alloc] initWithEngine:myPHASEEngine
    settings:pauseMenuDictionary timeToTarget:1 timeToReset:1];

// Create a settings dictionary for the in-game experience.
NSMutableDictionary<PHASEGroup*, PHASEGroupPresetSetting*> inGameDictionary;

// Enable volume only for in-game sounds.
[inGameDictionary setObject:groupSettingZeroVolume forKey:menuGroup]
[inGameDictionary setObject:groupSettingFullVolume forKey:bgmGroup]
[inGameDictionary setObject:groupSettingFullVolume forKey:voGroup]
PHASEGroupPreset* inGamePreset = [[PHASEGroupPreset alloc] initWithEngine:myPHASEEngine
    settings:inGameDictionary timeToTarget:1 timeToReset:1];

// Activate the pause menu preset when the user pauses the app.
[pauseMenuPreset activate];

// Activate the in-game preset when the user resumes the app. 
[inGamePreset activate];

// Clear the current preset by deactivating it.
[myPHASEEngine.activeGroupPreset deactivate]

TopicsCreating a Group Presetinit(engine: PHASEEngine, settings: [String : PHASEGroupPresetSetting], timeToTarget: Double, timeToReset: Double)Creates a group preset with the designated engine, settings, and fade parameters.Applying Settingsvar settings: [String : PHASEGroupPresetSetting]A dictionary with preset setting values and group objects as keys.Fading Between Settingsvar timeToTarget: DoubleA duration in which the engine fades the settings from their original value to their new value.var timeToReset: DoubleA duration in which the framework restores the group’s original state.Activating a Group Presetfunc activate()Applies settings to the designated groups.func activate(timeToTargetOverride: Double)Applies settings with an overriden fade duration.Deactivating a Group Presetfunc deactivate()Reverts settings for the preset’s groups.func deactivate(timeToResetOverride: Double)Reverts settings for the preset’s groups using a timed adjustment.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSound Grouping and Managementclass PHASEGroupA container that shares audio parameters with a collection of sounds.class PHASEGroupPresetSettingSettings for group presets.class PHASEDuckerAn object that manages competing sounds.

### activate() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegrouppreset/activate()

PHASE  PHASEGroupPreset  activate() Instance Methodactivate()Applies settings to the designated groups.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func activate()DiscussionWhen you call this function, the framework assigns the group preset as the engine’s activeGroupPreset and deactivates the previous assignee, as needed. The settings take effect according to timeToTarget.See AlsoActivating a Group Presetfunc activate(timeToTargetOverride: Double)Applies settings with an overriden fade duration.

### activate(timeToTargetOverride:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegrouppreset/activate(timetotargetoverride:)

PHASE  PHASEGroupPreset  activate(timeToTargetOverride:) Instance Methodactivate(timeToTargetOverride:)Applies settings with an overriden fade duration.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func activate(timeToTargetOverride: Double) Parameters timeToTargetOverrideA duration in which the engine fades the settings from their original value to their new value. Overrides timeToTarget.See AlsoActivating a Group Presetfunc activate()Applies settings to the designated groups.

### deactivate() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegrouppreset/deactivate()

PHASE  PHASEGroupPreset  deactivate() Instance Methoddeactivate()Reverts settings for the preset’s groups.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func deactivate()DiscussionWhen you call this function, the framework restores the group’s default state by removing the preset’s settings. The settings fade over the timeToReset duration, and the engine removes the preset from activeGroupPreset.See AlsoDeactivating a Group Presetfunc deactivate(timeToResetOverride: Double)Reverts settings for the preset’s groups using a timed adjustment.

### deactivate(timeToResetOverride:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegrouppreset/deactivate(timetoresetoverride:)

PHASE  PHASEGroupPreset  deactivate(timeToResetOverride:) Instance Methoddeactivate(timeToResetOverride:)Reverts settings for the preset’s groups using a timed adjustment.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func deactivate(timeToResetOverride: Double) Parameters timeToResetOverrideA duration that overrides timeToReset, in which the engine restores the group’s original state.See AlsoDeactivating a Group Presetfunc deactivate()Reverts settings for the preset’s groups.

### init(engine:settings:timeToTarget:timeToReset:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegrouppreset/init(engine:settings:timetotarget:timetoreset:)

PHASE  PHASEGroupPreset  init(engine:settings:timeToTarget:timeToReset:) Initializerinit(engine:settings:timeToTarget:timeToReset:)Creates a group preset with the designated engine, settings, and fade parameters.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    engine: PHASEEngine,
    settings: [String : PHASEGroupPresetSetting],
    timeToTarget: Double,
    timeToReset: Double
) Parameters engineAn engine containing groups to configure with settings.settingsA dictionary with preset setting values and group objects as keys. See settings.timeToTargetA duration in which the engine fades the settings from their original value to their new value. See timeToTarget.timeToResetA duration in which the framework restores the group’s original state. See timeToReset.

### settings | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegrouppreset/settings

PHASE  PHASEGroupPreset  settings Instance PropertysettingsA dictionary with preset setting values and group objects as keys.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var settings: [String : PHASEGroupPresetSetting] { get }DiscussionThis property defines the settings and the engine’s groups that receive the settings.

### timeToReset | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegrouppreset/timetoreset

PHASE  PHASEGroupPreset  timeToReset Instance PropertytimeToResetA duration in which the framework restores the group’s original state.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var timeToReset: Double { get }DiscussionThis property determines the speed of deactivation when the app calls deactivate(). The framework scales the value by unitsPerSecond.See AlsoFading Between Settingsvar timeToTarget: DoubleA duration in which the engine fades the settings from their original value to their new value.

### timeToTarget | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegrouppreset/timetotarget

PHASE  PHASEGroupPreset  timeToTarget Instance PropertytimeToTargetA duration in which the engine fades the settings from their original value to their new value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var timeToTarget: Double { get }DiscussionThis property determines the speed of activation when the app calls activate(). The framework scales the value by unitsPerSecond.See AlsoFading Between Settingsvar timeToReset: DoubleA duration in which the framework restores the group’s original state.

## PHASEGroupPresetSetting | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegrouppresetsetting

PHASE  PHASEGroupPresetSetting ClassPHASEGroupPresetSettingSettings for group presets.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEGroupPresetSettingOverviewThis class defines playback speed and volume rates of change that an app can apply to groups. To create a group preset setting, instantiate an object of this type and pass it to the settings parameter of init(engine:settings:timeToTarget:timeToReset:).For an example of preset settings, see PHASEGroupPreset.TopicsCreating a Settinginit(gain: Double, rate: Double, gainCurveType: PHASECurveType, rateCurveType: PHASECurveType)Creates a group preset setting.Setting Loudnessvar gain: DoubleThe volume of audio playback.var gainCurveType: PHASECurveTypeA rate of change for the setting’s volume.Setting Playback Speedvar rate: DoubleThe playback speed for audio.var rateCurveType: PHASECurveTypeA rate of change for the setting’s playback speed.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSound Grouping and Managementclass PHASEGroupA container that shares audio parameters with a collection of sounds.class PHASEGroupPresetA collection of settings for groups.class PHASEDuckerAn object that manages competing sounds.

### gain | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegrouppresetsetting/gain

PHASE  PHASEGroupPresetSetting  gain Instance PropertygainThe volume of audio playback.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var gain: Double { get }DiscussionThe framework sets the value to the init(gain:rate:gainCurveType:rateCurveType:) parameter, clamped to the range between 0 and 1. A value of 0 silences the audio and 1 doesn’t modify the audio’s original volume.See AlsoSetting Loudnessvar gainCurveType: PHASECurveTypeA rate of change for the setting’s volume.

### gainCurveType | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegrouppresetsetting/gaincurvetype

PHASE  PHASEGroupPresetSetting  gainCurveType Instance PropertygainCurveTypeA rate of change for the setting’s volume.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var gainCurveType: PHASECurveType { get }DiscussionThe framework sets the value to the init(gain:rate:gainCurveType:rateCurveType:) parameter.See AlsoSetting Loudnessvar gain: DoubleThe volume of audio playback.

### init(gain:rate:gainCurveType:rateCurveType:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegrouppresetsetting/init(gain:rate:gaincurvetype:ratecurvetype:)

PHASE  PHASEGroupPresetSetting  init(gain:rate:gainCurveType:rateCurveType:) Initializerinit(gain:rate:gainCurveType:rateCurveType:)Creates a group preset setting.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    gain: Double,
    rate: Double,
    gainCurveType: PHASECurveType,
    rateCurveType: PHASECurveType
) Parameters gainThe volume of audio playback. See gain.rateThe playback speed for audio. See rate.gainCurveTypeA rate of change for the setting’s volume.rateCurveTypeA rate of change for the setting’s playback speed.

### rate | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegrouppresetsetting/rate

PHASE  PHASEGroupPresetSetting  rate Instance PropertyrateThe playback speed for audio.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var rate: Double { get }DiscussionThe framework sets the value to the init(gain:rate:gainCurveType:rateCurveType:) parameter.See AlsoSetting Playback Speedvar rateCurveType: PHASECurveTypeA rate of change for the setting’s playback speed.

### rateCurveType | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasegrouppresetsetting/ratecurvetype

PHASE  PHASEGroupPresetSetting  rateCurveType Instance PropertyrateCurveTypeA rate of change for the setting’s playback speed.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var rateCurveType: PHASECurveType { get }DiscussionThe framework sets the value to the init(gain:rate:gainCurveType:rateCurveType:) parameter.See AlsoSetting Playback Speedvar rate: DoubleThe playback speed for audio.

## PHASEListener | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaselistener

PHASE  PHASEListener ClassPHASEListenerA central point of reference that defines the location within the scene that’s most audible to the user.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEListener Mentioned in  Playing sound from a location in a 3D scene OverviewPHASE requires an instance of this class to play ambient or spatial audio. To output sound through an ambient mixer or spatial mixer, the app adds an instance of this class to a sound event by using PHASEMixerParameters.For an example that demonstrates listeners, see Playing sound from a location in a 3D scene.TopicsCreating a Listenerinit(engine: PHASEEngine)Creates a listener with the given engine.Adjusting Loudnessvar gain: DoubleModifies the volume of all audio playback for the listener’s mixers.Instance Propertiesvar automaticHeadTrackingFlags: PHASEAutomaticHeadTrackingFlagsRelationshipsInherits FromPHASEObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSCopyingNSObjectProtocolSee AlsoSoundscape Creationclass PHASESourceAn object that plays audio from a 3D location and orientation in a scene.class PHASEOccluderAn object with a shape and position that blocks audio from reaching the listener.class PHASEObjectAn object in the scene.class PHASEShapeA collection of points that connect to form a 3D volume.class ElementAn object that describes the characteristics of a physical surface.class PHASEMaterialSurface characteristics that determine the acoustic properties of an object.enum PHASEMaterialPresetA collection of physical surfaces that each add a unique acoustic quality to your app’s audio.class PHASEMixerParametersAn object that specifies a mixer for sound events and orients them in 3D space.

### automaticHeadTrackingFlags | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaselistener/automaticheadtrackingflags

PHASE  PHASEListener  automaticHeadTrackingFlags Instance PropertyautomaticHeadTrackingFlagsiOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 26.0+Betavar automaticHeadTrackingFlags: PHASEAutomaticHeadTrackingFlags { get set }DiscussionA combination of flags to express automatic headtracking behaviors for this listener.Beta Software This documentation contains preliminary information about an API or technology in development. This information is subject to change, and software implemented according to this documentation should be tested with final operating system software.  Learn more about using Apple's beta software

### gain | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaselistener/gain

PHASE  PHASEListener  gain Instance PropertygainModifies the volume of all audio playback for the listener’s mixers.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var gain: Double { get set }DiscussionFor mixers that require a listener, this property modifies the volume of all audio the framework plays back through the listener by way of the listener’s associated mixers. The framework clamps the value to the range between 0 and 1, where 0 silences the audio and 1 doesn’t modify the audio’s original volume.

### init(engine:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaselistener/init(engine:)

PHASE  PHASEListener  init(engine:) Initializerinit(engine:)Creates a listener with the given engine.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(engine: PHASEEngine) Parameters engineThe object that controls the app’s audio output.

## PHASEMappedMetaParameterDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemappedmetaparameterdefinition

PHASE  PHASEMappedMetaParameterDefinition ClassPHASEMappedMetaParameterDefinitionA metaparameter that graphs an input value on a set of mathematical curves.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEMappedMetaParameterDefinitionOverviewThis class takes a metaparameter as input and plots its value on a curve defined by the envelope property.Whereas the envelope’s function in PHASEBlendNodeDefinition and PHASEEnvelopeDistanceModelParameters takes time because the relevant audio starts as its input parameter, in the case of the envelope property for this class, the app has full control over the input metaparameter’s value.TopicsCreating a Mapped Metaparameterinit(inputMetaParameterDefinition: PHASENumberMetaParameterDefinition, envelope: PHASEEnvelope)Creates a specification for a metaparameter that the app plots on a graph defined by the given set of curves.convenience init(inputMetaParameterDefinition: PHASENumberMetaParameterDefinition, envelope: PHASEEnvelope, identifier: String)Creates a specification for a named metaparameter that the app plots on a graph defined by the given set of curves.Inspecting the Input Parametervar inputMetaParameterDefinition: PHASENumberMetaParameterDefinitionA linear input value to plot on a curve.Inspecting the Envelopevar envelope: PHASEEnvelopeA collection of line segments that curve and connect to form a graph.RelationshipsInherits FromPHASENumberMetaParameterDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocol

### envelope | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemappedmetaparameterdefinition/envelope

PHASE  PHASEMappedMetaParameterDefinition  envelope Instance PropertyenvelopeA collection of line segments that curve and connect to form a graph.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var envelope: PHASEEnvelope { get }DiscussionThe line segments collectively plot an output value for the inputMetaParameterDefinition property.To plot the input, call evaluate(x:), passing in the input metaparameter’s value.To gradually change the input over time, call fade(value:duration:).

### init(inputMetaParameterDefinition:envelope:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemappedmetaparameterdefinition/init(inputmetaparameterdefinition:envelope:)

PHASE  PHASEMappedMetaParameterDefinition  init(inputMetaParameterDefinition:envelope:) Initializerinit(inputMetaParameterDefinition:envelope:)Creates a specification for a metaparameter that the app plots on a graph defined by the given set of curves.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    inputMetaParameterDefinition: PHASENumberMetaParameterDefinition,
    envelope: PHASEEnvelope
) Parameters inputMetaParameterDefinitionA metaparameter that contains an input value.envelopeA set of curves that graph the input value.See AlsoCreating a Mapped Metaparameterconvenience init(inputMetaParameterDefinition: PHASENumberMetaParameterDefinition, envelope: PHASEEnvelope, identifier: String)Creates a specification for a named metaparameter that the app plots on a graph defined by the given set of curves.

### init(inputMetaParameterDefinition:envelope:identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemappedmetaparameterdefinition/init(inputmetaparameterdefinition:envelope:identifier:)

PHASE  PHASEMappedMetaParameterDefinition  init(inputMetaParameterDefinition:envelope:identifier:) Initializerinit(inputMetaParameterDefinition:envelope:identifier:)Creates a specification for a named metaparameter that the app plots on a graph defined by the given set of curves.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+convenience init(
    inputMetaParameterDefinition: PHASENumberMetaParameterDefinition,
    envelope: PHASEEnvelope,
    identifier: String
) Parameters inputMetaParameterDefinitionA metaparameter that contains an input value.envelopeA set of curves that graph the input value.identifierA unique name for the metaparameter specification.See AlsoCreating a Mapped Metaparameterinit(inputMetaParameterDefinition: PHASENumberMetaParameterDefinition, envelope: PHASEEnvelope)Creates a specification for a metaparameter that the app plots on a graph defined by the given set of curves.

### inputMetaParameterDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemappedmetaparameterdefinition/inputmetaparameterdefinition

PHASE  PHASEMappedMetaParameterDefinition  inputMetaParameterDefinition Instance PropertyinputMetaParameterDefinitionA linear input value to plot on a curve.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var inputMetaParameterDefinition: PHASENumberMetaParameterDefinition { get }DiscussionThis property defines the input value to plot on a graph defined by envelope.To retrieve the output value, an app passes the metaparameter’s value to the evaluate(x:) function.

## PHASEMaterial | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasematerial

PHASE  PHASEMaterial ClassPHASEMaterialSurface characteristics that determine the acoustic properties of an object.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEMaterial Mentioned in  Playing sound from a location in a 3D scene OverviewTo specify the physical texture of a sound source or occluder, define the materials argument of the PHASEShape initializer, init(engine:mesh:materials:). The PHASEMaterialPreset contains the surface types with which you define the preset argument of this class’s init(engine:preset:) initializer.TopicsCreating a Materialinit(engine: PHASEEngine, preset: PHASEMaterialPreset)Creates a material with the given preset.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSoundscape Creationclass PHASESourceAn object that plays audio from a 3D location and orientation in a scene.class PHASEListenerA central point of reference that defines the location within the scene that’s most audible to the user.class PHASEOccluderAn object with a shape and position that blocks audio from reaching the listener.class PHASEObjectAn object in the scene.class PHASEShapeA collection of points that connect to form a 3D volume.class ElementAn object that describes the characteristics of a physical surface.enum PHASEMaterialPresetA collection of physical surfaces that each add a unique acoustic quality to your app’s audio.class PHASEMixerParametersAn object that specifies a mixer for sound events and orients them in 3D space.

### init(engine:preset:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasematerial/init(engine:preset:)

PHASE  PHASEMaterial  init(engine:preset:) Initializerinit(engine:preset:)Creates a material with the given preset.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    engine: PHASEEngine,
    preset: PHASEMaterialPreset
) Parameters engineThe object that controls the app’s audio output.presetA specific material among preselected options.

## PHASEMaterialPreset | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasematerialpreset

PHASE  PHASEMaterialPreset EnumerationPHASEMaterialPresetA collection of physical surfaces that each add a unique acoustic quality to your app’s audio.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum PHASEMaterialPreset Mentioned in  Playing sound from a location in a 3D scene OverviewThis enumeration defines the types of surface texture that you choose for your scene’s objects. To assign a preset to a material, define the preset argument for the material’s init(engine:preset:) initializer.TopicsPresetscase brickA surface characteristic that produces the acoustic quality of brick.case cardboardA surface characteristic that produces the acoustic quality of cardboard.case concreteA surface characteristic that produces the acoustic quality of concrete.case drywallA surface characteristic that produces the acoustic quality of drywall.case glassA surface characteristic that produces the acoustic quality of glass.case woodA surface characteristic that produces the acoustic quality of wood.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoSoundscape Creationclass PHASESourceAn object that plays audio from a 3D location and orientation in a scene.class PHASEListenerA central point of reference that defines the location within the scene that’s most audible to the user.class PHASEOccluderAn object with a shape and position that blocks audio from reaching the listener.class PHASEObjectAn object in the scene.class PHASEShapeA collection of points that connect to form a 3D volume.class ElementAn object that describes the characteristics of a physical surface.class PHASEMaterialSurface characteristics that determine the acoustic properties of an object.class PHASEMixerParametersAn object that specifies a mixer for sound events and orients them in 3D space.

### PHASEMaterialPreset.brick | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasematerialpreset/brick

PHASE  PHASEMaterialPreset  PHASEMaterialPreset.brick CasePHASEMaterialPreset.brickA surface characteristic that produces the acoustic quality of brick.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case brickSee AlsoPresetscase cardboardA surface characteristic that produces the acoustic quality of cardboard.case concreteA surface characteristic that produces the acoustic quality of concrete.case drywallA surface characteristic that produces the acoustic quality of drywall.case glassA surface characteristic that produces the acoustic quality of glass.case woodA surface characteristic that produces the acoustic quality of wood.

### PHASEMaterialPreset.cardboard | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasematerialpreset/cardboard

PHASE  PHASEMaterialPreset  PHASEMaterialPreset.cardboard CasePHASEMaterialPreset.cardboardA surface characteristic that produces the acoustic quality of cardboard.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case cardboardSee AlsoPresetscase brickA surface characteristic that produces the acoustic quality of brick.case concreteA surface characteristic that produces the acoustic quality of concrete.case drywallA surface characteristic that produces the acoustic quality of drywall.case glassA surface characteristic that produces the acoustic quality of glass.case woodA surface characteristic that produces the acoustic quality of wood.

### PHASEMaterialPreset.concrete | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasematerialpreset/concrete

PHASE  PHASEMaterialPreset  PHASEMaterialPreset.concrete CasePHASEMaterialPreset.concreteA surface characteristic that produces the acoustic quality of concrete.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case concreteSee AlsoPresetscase brickA surface characteristic that produces the acoustic quality of brick.case cardboardA surface characteristic that produces the acoustic quality of cardboard.case drywallA surface characteristic that produces the acoustic quality of drywall.case glassA surface characteristic that produces the acoustic quality of glass.case woodA surface characteristic that produces the acoustic quality of wood.

### PHASEMaterialPreset.drywall | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasematerialpreset/drywall

PHASE  PHASEMaterialPreset  PHASEMaterialPreset.drywall CasePHASEMaterialPreset.drywallA surface characteristic that produces the acoustic quality of drywall.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case drywallSee AlsoPresetscase brickA surface characteristic that produces the acoustic quality of brick.case cardboardA surface characteristic that produces the acoustic quality of cardboard.case concreteA surface characteristic that produces the acoustic quality of concrete.case glassA surface characteristic that produces the acoustic quality of glass.case woodA surface characteristic that produces the acoustic quality of wood.

### PHASEMaterialPreset.glass | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasematerialpreset/glass

PHASE  PHASEMaterialPreset  PHASEMaterialPreset.glass CasePHASEMaterialPreset.glassA surface characteristic that produces the acoustic quality of glass.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case glassSee AlsoPresetscase brickA surface characteristic that produces the acoustic quality of brick.case cardboardA surface characteristic that produces the acoustic quality of cardboard.case concreteA surface characteristic that produces the acoustic quality of concrete.case drywallA surface characteristic that produces the acoustic quality of drywall.case woodA surface characteristic that produces the acoustic quality of wood.

### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasematerialpreset/init(rawvalue:)

PHASE  PHASEMaterialPreset  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

### PHASEMaterialPreset.wood | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasematerialpreset/wood

PHASE  PHASEMaterialPreset  PHASEMaterialPreset.wood CasePHASEMaterialPreset.woodA surface characteristic that produces the acoustic quality of wood.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case woodSee AlsoPresetscase brickA surface characteristic that produces the acoustic quality of brick.case cardboardA surface characteristic that produces the acoustic quality of cardboard.case concreteA surface characteristic that produces the acoustic quality of concrete.case drywallA surface characteristic that produces the acoustic quality of drywall.case glassA surface characteristic that produces the acoustic quality of glass.

## PHASEMedium | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemedium

PHASE  PHASEMedium ClassPHASEMediumA property or quality of the environment that affects how sound travels.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEMediumOverviewThis class defines choices for the engine’s defaultMedium. Currently, this property provides only sound traveling through air.TopicsCreating a Mediuminit(engine: PHASEEngine, preset: PHASEMedium.Preset)Creates a medium.enum PresetPredetermined qualities of an environment that affect how sound transmits.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSetupclass PHASEEngineAn object that manages audio assets, controls playback, and configures environmental effects.enum UpdateModeModes that determine when the framework consumes API calls and updates internal state.enum RenderingModeModes that determine whether the system renders audio in process or out of process.Betaclass PHASEAssetRegistryA central repository of audio assets.enum PHASENormalizationModeOptions that determine whether the framework adjusts a sound asset’s loudness for the user’s output device.enum PHASESpatializationModeThe manner in which PHASE outputs spatial audio.enum PHASEReverbPresetThe manner in which PHASE diffuses resonating sound.

### init(engine:preset:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemedium/init(engine:preset:)

PHASE  PHASEMedium  init(engine:preset:) Initializerinit(engine:preset:)Creates a medium.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    engine: PHASEEngine,
    preset: PHASEMedium.Preset
) Parameters engineThe framework engine object.presetA predefined option for the medium.See AlsoCreating a Mediumenum PresetPredetermined qualities of an environment that affect how sound transmits.

### PHASEMedium.Preset | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemedium/preset

PHASE  PHASEMedium  PHASEMedium.Preset EnumerationPHASEMedium.PresetPredetermined qualities of an environment that affect how sound transmits.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum PresetOverviewCurrently, this enumeration refers only to sound traveling through air.TopicsMedium Typescase airA medium that simulates sound traveling through air.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoCreating a Mediuminit(engine: PHASEEngine, preset: PHASEMedium.Preset)Creates a medium.

#### PHASEMedium.Preset.air | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemedium/preset/air

PHASE  PHASEMedium  PHASEMedium  PHASEMedium.Preset  PHASEMedium.Preset.air CasePHASEMedium.Preset.airA medium that simulates sound traveling through air.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case air

#### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemedium/preset/init(rawvalue:)

PHASE  PHASEMedium  PHASEMedium  PHASEMedium.Preset  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

## PHASEMetaParameter | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemetaparameter

PHASE  PHASEMetaParameter ClassPHASEMetaParameterA named parameter with a value that the app can change over time.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEMetaParameterOverviewInstances of this class provide an app with dynamic control of a sound’s properties. A metaparameter takes a single value as input and may operate on one or more audio characteristics.To change the value of a metaparameter at runtime:Assign a string to a textual metaparameter’s value.Adjust the value of a number or mapped metaparameter gradually over a duration by calling fade(value:duration:).TopicsAccessing the Valuevar value: AnyA value for the metaparameter.Identifying the Parametervar identifier: StringA unique name for the metaparameter.RelationshipsInherits FromNSObjectInherited ByPHASENumberMetaParameterPHASEStringMetaParameterConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoBase Metaparametersclass PHASEMetaParameterDefinitionA specification for a named parameter with a constant value.class PHASEGlobalMetaParameterAssetA reference to a registered metaparameter that the app can share with multiple sound events or sources.

### identifier | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemetaparameter/identifier

PHASE  PHASEMetaParameter  identifier Instance PropertyidentifierA unique name for the metaparameter.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var identifier: String { get }

### value | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemetaparameter/value

PHASE  PHASEMetaParameter  value Instance PropertyvalueA value for the metaparameter.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var value: Any { get set }DiscussionThe framework sets this property to the subclass’s initializer argument; for example, see init(value:).An app changes the value at runtime by calling fade(value:duration:) on the subclass.

## PHASEMetaParameterDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemetaparameterdefinition

PHASE  PHASEMetaParameterDefinition ClassPHASEMetaParameterDefinitionA specification for a named parameter with a constant value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEMetaParameterDefinitionOverviewInstances of this class provide an app with dynamic control of various properies of live audio playback. This is a base class for the PHASENumberMetaParameterDefinition and PHASEStringMetaParameterDefinition subclasses.You create a single instance of one of the subclasses for a specific property you want to adjust. By passing the definition subclass to the framework, you spawn one or more PHASEMetaParameterDefinition objects for discrete use across your app. For example, when you initialize a PHASEBlendNodeDefinition with a number metaparameter definition, PHASE registers a PHASENumberMetaParameter in the corresponding sound event’s metaParameters dictionary.Put metaparameter definitions that you wish to share across different sounds in the asset registery’s globalMetaParameters dictionary. To add global metaparameter definitions to the dictionary, call  registerGlobalMetaParameter(metaParameterDefinition:). Then pass the definition into several sound event node defintions, such as PHASESamplerNodeDefinition.TopicsSetting a Metaparametervar value: AnyA constant value for the parameter definition.RelationshipsInherits FromPHASEDefinitionInherited ByPHASENumberMetaParameterDefinitionPHASEStringMetaParameterDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoBase Metaparametersclass PHASEMetaParameterA named parameter with a value that the app can change over time.class PHASEGlobalMetaParameterAssetA reference to a registered metaparameter that the app can share with multiple sound events or sources.

### value | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemetaparameterdefinition/value

PHASE  PHASEMetaParameterDefinition  value Instance PropertyvalueA constant value for the parameter definition.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var value: Any { get }DiscussionSet this value using a subclass initializer. For example, see init(value:).

## PHASEMixer | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemixer

PHASE  PHASEMixer ClassPHASEMixerAn object that combines multiple audio signals into a single signal.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEMixerOverviewMixers provide a single point of control over the multiple audio signals they combine. To create a mixer, you provide the framework with a mixer definition; see PHASEMixerDefinition.Subclasses of this class define unique properties the app sets to control specific features. For example, the spatial mixer (PHASESpatialMixerDefinition) adds environmental effects into the output audio signal.TopicsAdjusting Volumevar gain: DoubleThe mixer’s volume.var gainMetaParameter: PHASEMetaParameter?A parameter that changes the mixer’s volume gradually over a period of time.Retrieving the Mixer Identifiervar identifier: StringA unique name for the mixer.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoAudio Layering and Effectsclass PHASEChannelMixerDefinitionAn audio-layering object that routes sound directly to the device’s output.class PHASEAmbientMixerDefinitionAn audio-layering object that outputs sound in a particular direction in 3D space.class PHASEMixerDefinitionAn object to initialize a mixer with a given configuration.class PHASEDefinitionA base class that adds a name to framework definitions.API ReferenceSpatial MixingDefine environmental characteristics that determine how sound plays in your app’s 3D soundscape.

### gain | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemixer/gain

PHASE  PHASEMixer  gain Instance PropertygainThe mixer’s volume.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var gain: Double { get }DiscussionThe framework clamps the value to the range between 0 and 1, where 0 silences the mixer’s volume and 1 doesn’t modify the volume.See AlsoAdjusting Volumevar gainMetaParameter: PHASEMetaParameter?A parameter that changes the mixer’s volume gradually over a period of time.

### gainMetaParameter | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemixer/gainmetaparameter

PHASE  PHASEMixer  gainMetaParameter Instance PropertygainMetaParameterA parameter that changes the mixer’s volume gradually over a period of time.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var gainMetaParameter: PHASEMetaParameter? { get }DiscussionUse this property to smoothly adjust the volume of the mixer’s audio signals by calling fade(value:duration:).The framework sets the initial value of this property according to the metaparameter definition object’s gainMetaParameterDefinition.See AlsoAdjusting Volumevar gain: DoubleThe mixer’s volume.

### identifier | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemixer/identifier

PHASE  PHASEMixer  identifier Instance PropertyidentifierA unique name for the mixer.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var identifier: String { get }

## PHASEMixerDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemixerdefinition

PHASE  PHASEMixerDefinition ClassPHASEMixerDefinitionAn object to initialize a mixer with a given configuration.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEMixerDefinitionOverviewA mixer combines multiple layers of audio to a single signal for transmission to the output device. The framework creates a mixer when you provide a mixer definition. Instead of creating an instance of this class, instantiate one of the mixer definition subclasses instead:PHASEChannelMixerDefinitionWhen your app outputs sound through a channel mixer, the framework maintains the channel configuration of the source audio. For example, the left and right channels of a stereo input file play on the left and right speakers, respectively.PHASEAmbientMixerDefinitionWhen your app outputs sound through an ambient mixer, the framework overrides the output channels to give the mixer an orientation, which creates the effect of pointing in a specific direction in 3D space.PHASESpatialMixerDefinitionAudio that your app outputs through a spatial mixer specifies a position and orientation in 3D space. Spatial mixers require the app to define sources that emit audio, and a listener that hears audio. Sound playback changes depending on the relative positions of the listener and sources.Play a Sound Using a MixerTo play a sound using a mixer, create a mixer definition and pass it to a sound event. The following code creates a PHASEChannelMixerDefinition and passes it into a node definition the app can invoke to play the channel-based audio file drumloopSoundAsset:// Create a channel mixer definition.
let stereoMixer = PHASEChannelMixerDefinition(channelLayout:stereoLayout!)

// Pass the mixer to a sound event node definition that plays an audio file.
let drumloopSamplerNode = PHASESamplerNodeDefinition(soundAssetIdentifier:drumloopSoundAsset.identifier, mixerDefinition:stereoMixer, identifier:"drumloopNode")
TopicsControlling Volumevar gain: DoubleThe mixer’s volume.var gainMetaParameterDefinition: PHASENumberMetaParameterDefinition?A template for a parameter that changes the mixer’s volume gradually over a period of time.RelationshipsInherits FromPHASEDefinitionInherited ByPHASEAmbientMixerDefinitionPHASEChannelMixerDefinitionPHASESpatialMixerDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoAudio Layering and Effectsclass PHASEChannelMixerDefinitionAn audio-layering object that routes sound directly to the device’s output.class PHASEAmbientMixerDefinitionAn audio-layering object that outputs sound in a particular direction in 3D space.class PHASEMixerAn object that combines multiple audio signals into a single signal.class PHASEDefinitionA base class that adds a name to framework definitions.API ReferenceSpatial MixingDefine environmental characteristics that determine how sound plays in your app’s 3D soundscape.

### gain | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemixerdefinition/gain

PHASE  PHASEMixerDefinition  gain Instance PropertygainThe mixer’s volume.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var gain: Double { get set }DiscussionThis property modifies the volume of all the mixer’s audio in the output’s final stages. The framework clamps the value to the range between 0 and 1, where 0 silences the audio and 1 doesn’t modify the audio’s original volume.See AlsoControlling Volumevar gainMetaParameterDefinition: PHASENumberMetaParameterDefinition?A template for a parameter that changes the mixer’s volume gradually over a period of time.

### gainMetaParameterDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemixerdefinition/gainmetaparameterdefinition

PHASE  PHASEMixerDefinition  gainMetaParameterDefinition Instance PropertygainMetaParameterDefinitionA template for a parameter that changes the mixer’s volume gradually over a period of time.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var gainMetaParameterDefinition: PHASENumberMetaParameterDefinition? { get set }DiscussionWhen the framework creates a mixer from a mixer definition, PHASE initializes the mixer’s gainMetaParameter to this property’s values.See AlsoControlling Volumevar gain: DoubleThe mixer’s volume.

## PHASEMixerParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemixerparameters

PHASE  PHASEMixerParameters ClassPHASEMixerParametersAn object that specifies a mixer for sound events and orients them in 3D space.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEMixerParameters Mentioned in  Playing sound from a location in a 3D scene OverviewThis class orients a sound event in 3D space relative to a listener. When you configure an ambient mixer’s orientation and a listener’s orientation, PHASE lowers the volume of the sound event if the two orientations point away from each other, and plays the sound at full volume if they point at each other. To add an instance of this class to a sound event, use the mixerParameters argument of a sound event’s init(engine:assetIdentifier:mixerParameters:) initializer.Alternatively, PHASE can adjust a sound event’s loudness based on its distance from the listener in 3D space. By calling this class’s addSpatialMixerParameters(identifier:source:listener:) function, you supply a sound source that defines the location. For more information, see Spatial Mixing.Ambient sound events define only a listener and play with a consistent loudness, regardless of the listener’s position in the scene. To define a listener and select a particular ambient mixer that outputs the sound, call this class’s addAmbientMixerParameters(identifier:listener:) function.TopicsPositioning and Orienting Audiofunc addAmbientMixerParameters(identifier: String, listener: PHASEListener)Adds runtime parameters for an ambient mixer.func addSpatialMixerParameters(identifier: String, source: PHASESource, listener: PHASEListener)Adds runtime parameters for a spatial mixer.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSoundscape Creationclass PHASESourceAn object that plays audio from a 3D location and orientation in a scene.class PHASEListenerA central point of reference that defines the location within the scene that’s most audible to the user.class PHASEOccluderAn object with a shape and position that blocks audio from reaching the listener.class PHASEObjectAn object in the scene.class PHASEShapeA collection of points that connect to form a 3D volume.class ElementAn object that describes the characteristics of a physical surface.class PHASEMaterialSurface characteristics that determine the acoustic properties of an object.enum PHASEMaterialPresetA collection of physical surfaces that each add a unique acoustic quality to your app’s audio.

### addAmbientMixerParameters(identifier:listener:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemixerparameters/addambientmixerparameters(identifier:listener:)

PHASE  PHASEMixerParameters  addAmbientMixerParameters(identifier:listener:) Instance MethodaddAmbientMixerParameters(identifier:listener:)Adds runtime parameters for an ambient mixer.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func addAmbientMixerParameters(
    identifier: String,
    listener: PHASEListener
) Parameters identifierThe name of the spatial submixer.listenerAn object that receives a source audio signal. The mixer orients the sound the listener receives based on its transform.See AlsoPositioning and Orienting Audiofunc addSpatialMixerParameters(identifier: String, source: PHASESource, listener: PHASEListener)Adds runtime parameters for a spatial mixer.

### addSpatialMixerParameters(identifier:source:listener:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasemixerparameters/addspatialmixerparameters(identifier:source:listener:)

PHASE  PHASEMixerParameters  addSpatialMixerParameters(identifier:source:listener:) Instance MethodaddSpatialMixerParameters(identifier:source:listener:)Adds runtime parameters for a spatial mixer.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func addSpatialMixerParameters(
    identifier: String,
    source: PHASESource,
    listener: PHASEListener
) Parameters identifierThe name of the spatial submixer.sourceA location in the scene that plays audio.listenerAn object that receives a source audio signal. The mixer scales and orients the sound the listener receives based on its transform.See AlsoPositioning and Orienting Audiofunc addAmbientMixerParameters(identifier: String, listener: PHASEListener)Adds runtime parameters for an ambient mixer.

## PHASENormalizationMode | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenormalizationmode

PHASE  PHASENormalizationMode EnumerationPHASENormalizationModeOptions that determine whether the framework adjusts a sound asset’s loudness for the user’s output device.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum PHASENormalizationModeOverviewDifferent output devices feature loudness characteristics that require the audio engine to adjust the volume of the input audio to achieve a consistent listening experience across devices.PHASE callibrates sound asset and stream loudness automatically when the app chooses PHASENormalizationMode.dynamic. If an app chooses PHASENormalizationMode.none, the app needs to implement custom loudness normalizaton manually, by adjusting sound asset and stream signal strength for the user’s output device.TopicsLoudness Normalization Modescase dynamicA mode that instructs the framework to adjust a sound’s volume according to the user’s output device.case noneA mode that instructs the framework not to adjust a sound’s volume according to the user’s output device.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoSetupclass PHASEEngineAn object that manages audio assets, controls playback, and configures environmental effects.enum UpdateModeModes that determine when the framework consumes API calls and updates internal state.enum RenderingModeModes that determine whether the system renders audio in process or out of process.Betaclass PHASEAssetRegistryA central repository of audio assets.enum PHASESpatializationModeThe manner in which PHASE outputs spatial audio.enum PHASEReverbPresetThe manner in which PHASE diffuses resonating sound.class PHASEMediumA property or quality of the environment that affects how sound travels.

### PHASENormalizationMode.dynamic | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenormalizationmode/dynamic

PHASE  PHASENormalizationMode  PHASENormalizationMode.dynamic CasePHASENormalizationMode.dynamicA mode that instructs the framework to adjust a sound’s volume according to the user’s output device.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case dynamicDiscussionFor more information, see PHASENormalizationMode.See AlsoLoudness Normalization Modescase noneA mode that instructs the framework not to adjust a sound’s volume according to the user’s output device.

### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenormalizationmode/init(rawvalue:)

PHASE  PHASENormalizationMode  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

### PHASENormalizationMode.none | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenormalizationmode/none

PHASE  PHASENormalizationMode  PHASENormalizationMode.none CasePHASENormalizationMode.noneA mode that instructs the framework not to adjust a sound’s volume according to the user’s output device.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case noneDiscussionFor more information, see PHASENormalizationMode.See AlsoLoudness Normalization Modescase dynamicA mode that instructs the framework to adjust a sound’s volume according to the user’s output device.

## PHASENumberMetaParameter | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenumbermetaparameter

PHASE  PHASENumberMetaParameter ClassPHASENumberMetaParameterA metaparameter defined by a number that can change over time.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASENumberMetaParameterOverviewThis class contains a number that updates, like a “player speed” metaparameter that the app changes gradually from 0.0 to 1.0.To create an instance of this class, first create a PHASENumberMetaParameterDefinition, and either:Register it with the engine by calling registerGlobalMetaParameter(metaParameterDefinition:), then access the instance of this class in the engine’s globalMetaParameters dictionary.Pass it to the PHASEBlendNodeDefinition initializer, init(blendMetaParameterDefinition:identifier:), and then access the instance of this class in a sound event’s metaParameters dictionary.Use it as the input value for a PHASEMappedMetaParameterDefinition by passing it into the init(inputMetaParameterDefinition:envelope:) initializer. Then, access the instance of this class using the mapped parameter’s inputMetaParameterDefinition property.TopicsInspecting Extremesvar minimum: DoubleThe lowest possible number for the value.var maximum: DoubleThe highest possible number for the value.Interpolating the Valuefunc fade(value: Double, duration: TimeInterval)Sets the value gradually over the given amount of time.RelationshipsInherits FromPHASEMetaParameterConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoLinear Metaparametersclass PHASENumberMetaParameterDefinitionA specification for a metaparameter defined by a number.

### fade(value:duration:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenumbermetaparameter/fade(value:duration:)

PHASE  PHASENumberMetaParameter  fade(value:duration:) Instance Methodfade(value:duration:)Sets the value gradually over the given amount of time.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func fade(
    value: Double,
    duration: TimeInterval
) Parameters valueA new value for the metaparameter.durationAn amount of time in which the number gradually adjusts to the new value.

### maximum | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenumbermetaparameter/maximum

PHASE  PHASENumberMetaParameter  maximum Instance PropertymaximumThe highest possible number for the value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var maximum: Double { get }DiscussionThe framework sets the value to the metaparameter definition’s maximum property.See AlsoInspecting Extremesvar minimum: DoubleThe lowest possible number for the value.

### minimum | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenumbermetaparameter/minimum

PHASE  PHASENumberMetaParameter  minimum Instance PropertyminimumThe lowest possible number for the value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var minimum: Double { get }DiscussionThe framework sets the value to the metaparameter definition’s minimum property.See AlsoInspecting Extremesvar maximum: DoubleThe highest possible number for the value.

## PHASENumberMetaParameterDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenumbermetaparameterdefinition

PHASE  PHASENumberMetaParameterDefinition ClassPHASENumberMetaParameterDefinitionA specification for a metaparameter defined by a number.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASENumberMetaParameterDefinitionOverviewUse this class to spawn discrete instances of PHASENumberMetaParameter, for example, a “player speed” metaparameter that the app changes gradually from 0.0 to 1.0.To use a number metaparameter, create an instance of this class and:Register it with the engine by calling registerGlobalMetaParameter(metaParameterDefinition:), then access the instance of this class in the engine’s globalMetaParameters dictionary.Pass it to the PHASEBlendNodeDefinition initializer, init(blendMetaParameterDefinition:identifier:), and then access the instance of this class in a sound event’s metaParameters dictionary.Pass it into the PHASEMappedMetaParameterDefinition initializer, init(inputMetaParameterDefinition:envelope:). Then, access the instance of this class using the mapped parameter’s inputMetaParameterDefinition property.TopicsCreating a Metaparameter Definitionconvenience init(value: Double)Creates a specification for a metaparameter with the given numeric value.convenience init(value: Double, identifier: String)Creates a specification for a named metaparameter with the given numeric value.init(value: Double, minimum: Double, maximum: Double)Creates a specification for a metaparameter with the given numeric value and range.convenience init(value: Double, minimum: Double, maximum: Double, identifier: String)Creates a specification for a named metaparameter with the given numeric value and range.Reistricting the Valuevar minimum: DoubleThe lowest possible number for the value.var maximum: DoubleThe highest possible number for the value.RelationshipsInherits FromPHASEMetaParameterDefinitionInherited ByPHASEMappedMetaParameterDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoLinear Metaparametersclass PHASENumberMetaParameterA metaparameter defined by a number that can change over time.

### init(value:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenumbermetaparameterdefinition/init(value:)

PHASE  PHASENumberMetaParameterDefinition  init(value:) Initializerinit(value:)Creates a specification for a metaparameter with the given numeric value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+convenience init(value: Double) Parameters valueA default value for the metaparameter specification.See AlsoCreating a Metaparameter Definitionconvenience init(value: Double, identifier: String)Creates a specification for a named metaparameter with the given numeric value.init(value: Double, minimum: Double, maximum: Double)Creates a specification for a metaparameter with the given numeric value and range.convenience init(value: Double, minimum: Double, maximum: Double, identifier: String)Creates a specification for a named metaparameter with the given numeric value and range.

### init(value:identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenumbermetaparameterdefinition/init(value:identifier:)

PHASE  PHASENumberMetaParameterDefinition  init(value:identifier:) Initializerinit(value:identifier:)Creates a specification for a named metaparameter with the given numeric value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+convenience init(
    value: Double,
    identifier: String
) Parameters valueA default value for the metaparameter specification.identifierA unique name for the metaparameter specification.See AlsoCreating a Metaparameter Definitionconvenience init(value: Double)Creates a specification for a metaparameter with the given numeric value.init(value: Double, minimum: Double, maximum: Double)Creates a specification for a metaparameter with the given numeric value and range.convenience init(value: Double, minimum: Double, maximum: Double, identifier: String)Creates a specification for a named metaparameter with the given numeric value and range.

### init(value:minimum:maximum:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenumbermetaparameterdefinition/init(value:minimum:maximum:)

PHASE  PHASENumberMetaParameterDefinition  init(value:minimum:maximum:) Initializerinit(value:minimum:maximum:)Creates a specification for a metaparameter with the given numeric value and range.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    value: Double,
    minimum: Double,
    maximum: Double
) Parameters valueA default value for the metaparameter specification.minimumThe lowest possible number for the value.maximumThe highest possible number for the value.See AlsoCreating a Metaparameter Definitionconvenience init(value: Double)Creates a specification for a metaparameter with the given numeric value.convenience init(value: Double, identifier: String)Creates a specification for a named metaparameter with the given numeric value.convenience init(value: Double, minimum: Double, maximum: Double, identifier: String)Creates a specification for a named metaparameter with the given numeric value and range.

### init(value:minimum:maximum:identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenumbermetaparameterdefinition/init(value:minimum:maximum:identifier:)

PHASE  PHASENumberMetaParameterDefinition  init(value:minimum:maximum:identifier:) Initializerinit(value:minimum:maximum:identifier:)Creates a specification for a named metaparameter with the given numeric value and range.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+convenience init(
    value: Double,
    minimum: Double,
    maximum: Double,
    identifier: String
) Parameters valueA default value for the metaparameter specification.minimumThe lowest possible number for the value.maximumThe highest possible number for the value.identifierA unique name for the metaparameter specification.See AlsoCreating a Metaparameter Definitionconvenience init(value: Double)Creates a specification for a metaparameter with the given numeric value.convenience init(value: Double, identifier: String)Creates a specification for a named metaparameter with the given numeric value.init(value: Double, minimum: Double, maximum: Double)Creates a specification for a metaparameter with the given numeric value and range.

### maximum | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenumbermetaparameterdefinition/maximum

PHASE  PHASENumberMetaParameterDefinition  maximum Instance PropertymaximumThe highest possible number for the value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var maximum: Double { get }DiscussionThe framework sets the value of this property to the init(value:minimum:maximum:) argument.See AlsoReistricting the Valuevar minimum: DoubleThe lowest possible number for the value.

### minimum | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenumbermetaparameterdefinition/minimum

PHASE  PHASENumberMetaParameterDefinition  minimum Instance PropertyminimumThe lowest possible number for the value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var minimum: Double { get }DiscussionThe framework sets the value of this property to the init(value:minimum:maximum:) argument.See AlsoReistricting the Valuevar maximum: DoubleThe highest possible number for the value.

## PHASENumericPair | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenumericpair

PHASE  PHASENumericPair ClassPHASENumericPairAn ordered pair that defines a bounding box for an envelope.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASENumericPairOverviewA PHASEEnvelope object uses this class to bound the value of its range and domain.TopicsCreating a Numeric Pairinit(firstValue: Double, secondValue: Double)Creates a pair of numbers with the given values.Defining the Valuesvar first: DoubleThe first value in the pair.var second: DoubleThe second value in the pair.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoDynamic Sound Controlclass PHASEEnvelopeA collection of segments that connect to graph a complex curve over a linear input.class PHASEEnvelopeSegmentA curved portion of an envelope.enum PHASECurveTypeOptions that apply a mathematical function to an input value.API ReferencePlayback ParameterizationChange the characteristics of in-flight audio by adjusting its properties at runtime.

### first | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenumericpair/first

PHASE  PHASENumericPair  first Instance PropertyfirstThe first value in the pair.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var first: Double { get set }See AlsoDefining the Valuesvar second: DoubleThe second value in the pair.

### init(firstValue:secondValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenumericpair/init(firstvalue:secondvalue:)

PHASE  PHASENumericPair  init(firstValue:secondValue:) Initializerinit(firstValue:secondValue:)Creates a pair of numbers with the given values.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    firstValue first: Double,
    secondValue second: Double
)

### second | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasenumericpair/second

PHASE  PHASENumericPair  second Instance PropertysecondThe second value in the pair.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var second: Double { get set }See AlsoDefining the Valuesvar first: DoubleThe first value in the pair.

## PHASEObject | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseobject

PHASE  PHASEObject ClassPHASEObjectAn object in the scene.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEObject Mentioned in  Playing sound from a location in a 3D scene OverviewThis class models a member of your app’s scene by defining a 3D position and orientation.The following subclasses derive from this class:PHASESourceAn object that plays audio from a 3D location and orientation in a scene.PHASEListenerA central point of reference that defines the area within the scene that’s most audible to the user.PHASEOccluderAn object with a shape and position that blocks audio from reaching the listener.The children array holds instances of this class to position and orient them relatively.TopicsCreating an Objectinit(engine: PHASEEngine)Creates an object in the scene.Managing the Hierarchyvar children: [PHASEObject]Objects that position and orient in the scene relative to the given object.var parent: PHASEObject?The object that this instance positions and orients relative to in the scene.func addChild(PHASEObject) throwsAdds the given object as a child.func removeChild(PHASEObject)Removes the given object as a child.func removeChildren()Removes all child objects from the given object.Defining a Posevar transform: simd_float4x4A matrix, in local coordinates, that determines the object’s pose in the scene.var worldTransform: simd_float4x4A matrix, in scene coordinates, that determines the object’s pose in the scene.Inspecting the Orientationclass var forward: simd_float3A vector that points forward in the local coordinate space.class var right: simd_float3A vector that points right in the local coordinate space.class var up: simd_float3A vector that points up in the local coordinate space.RelationshipsInherits FromNSObjectInherited ByPHASEListenerPHASEOccluderPHASESourceConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSCopyingNSObjectProtocolSee AlsoSoundscape Creationclass PHASESourceAn object that plays audio from a 3D location and orientation in a scene.class PHASEListenerA central point of reference that defines the location within the scene that’s most audible to the user.class PHASEOccluderAn object with a shape and position that blocks audio from reaching the listener.class PHASEShapeA collection of points that connect to form a 3D volume.class ElementAn object that describes the characteristics of a physical surface.class PHASEMaterialSurface characteristics that determine the acoustic properties of an object.enum PHASEMaterialPresetA collection of physical surfaces that each add a unique acoustic quality to your app’s audio.class PHASEMixerParametersAn object that specifies a mixer for sound events and orients them in 3D space.

### addChild(_:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseobject/addchild(_:)

PHASE  PHASEObject  addChild(_:) Instance MethodaddChild(_:)Adds the given object as a child.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func addChild(_ child: PHASEObject) throws Parameters childThe object to add to the children array. Mentioned in  Playing sound from a location in a 3D scene DiscussionThis function throws an error if child already has a different parent.See AlsoManaging the Hierarchyvar children: [PHASEObject]Objects that position and orient in the scene relative to the given object.var parent: PHASEObject?The object that this instance positions and orients relative to in the scene.func removeChild(PHASEObject)Removes the given object as a child.func removeChildren()Removes all child objects from the given object.

### children | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseobject/children

PHASE  PHASEObject  children Instance PropertychildrenObjects that position and orient in the scene relative to the given object.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var children: [PHASEObject] { get }DiscussionTo manage members of this array, use addChild(_:),  removeChild(_:), and removeChildren().See AlsoManaging the Hierarchyvar parent: PHASEObject?The object that this instance positions and orients relative to in the scene.func addChild(PHASEObject) throwsAdds the given object as a child.func removeChild(PHASEObject)Removes the given object as a child.func removeChildren()Removes all child objects from the given object.

### forward | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseobject/forward

PHASE  PHASEObject  forward Type PropertyforwardA vector that points forward in the local coordinate space.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class var forward: simd_float3 { get }See AlsoInspecting the Orientationclass var right: simd_float3A vector that points right in the local coordinate space.class var up: simd_float3A vector that points up in the local coordinate space.

### init(engine:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseobject/init(engine:)

PHASE  PHASEObject  init(engine:) Initializerinit(engine:)Creates an object in the scene.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(engine: PHASEEngine) Parameters engineThe object that controls the app’s audio output.

### parent | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseobject/parent

PHASE  PHASEObject  parent Instance PropertyparentThe object that this instance positions and orients relative to in the scene.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+weak var parent: PHASEObject? { get }See AlsoManaging the Hierarchyvar children: [PHASEObject]Objects that position and orient in the scene relative to the given object.func addChild(PHASEObject) throwsAdds the given object as a child.func removeChild(PHASEObject)Removes the given object as a child.func removeChildren()Removes all child objects from the given object.

### removeChild(_:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseobject/removechild(_:)

PHASE  PHASEObject  removeChild(_:) Instance MethodremoveChild(_:)Removes the given object as a child.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func removeChild(_ child: PHASEObject) Parameters childThe object to remove from the children array.See AlsoManaging the Hierarchyvar children: [PHASEObject]Objects that position and orient in the scene relative to the given object.var parent: PHASEObject?The object that this instance positions and orients relative to in the scene.func addChild(PHASEObject) throwsAdds the given object as a child.func removeChildren()Removes all child objects from the given object.

### removeChildren() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseobject/removechildren()

PHASE  PHASEObject  removeChildren() Instance MethodremoveChildren()Removes all child objects from the given object.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func removeChildren()DiscussionThis function removes all members from the children array.See AlsoManaging the Hierarchyvar children: [PHASEObject]Objects that position and orient in the scene relative to the given object.var parent: PHASEObject?The object that this instance positions and orients relative to in the scene.func addChild(PHASEObject) throwsAdds the given object as a child.func removeChild(PHASEObject)Removes the given object as a child.

### right | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseobject/right

PHASE  PHASEObject  right Type PropertyrightA vector that points right in the local coordinate space.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class var right: simd_float3 { get }See AlsoInspecting the Orientationclass var forward: simd_float3A vector that points forward in the local coordinate space.class var up: simd_float3A vector that points up in the local coordinate space.

### transform | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseobject/transform

PHASE  PHASEObject  transform Instance PropertytransformA matrix, in local coordinates, that determines the object’s pose in the scene.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var transform: simd_float4x4 { get set } Mentioned in  Playing sound from a location in a 3D scene DiscussionThe value of this property requires orthogonal basis vectors and uniform scale.The framework interprets the transform’s position values in a right-handed coordinate system, where the Y axis extends upward and and the negative Z axis extends forward.Set an Object’s PositionAn object positions in the 3D scene by the transformʼs first 3 elements of the last column. The following code sets an object’s position to (0,0,-6), which is 6 meters in front of the world origin (0,0,0).var boardPieceTransform: simd_float4x4 = matrix_identity_float4x4
boardPieceTransform.columns.3.z -= 6.0
boardPieceSource.transform = boardPieceTransform
Set the unitsPerMeter parameter to instruct PHASE to interpret transform values in your app’s preferred unit of measurement.See AlsoDefining a Posevar worldTransform: simd_float4x4A matrix, in scene coordinates, that determines the object’s pose in the scene.

### up | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseobject/up

PHASE  PHASEObject  up Type PropertyupA vector that points up in the local coordinate space.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class var up: simd_float3 { get }See AlsoInspecting the Orientationclass var forward: simd_float3A vector that points forward in the local coordinate space.class var right: simd_float3A vector that points right in the local coordinate space.

### worldTransform | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseobject/worldtransform

PHASE  PHASEObject  worldTransform Instance PropertyworldTransformA matrix, in scene coordinates, that determines the object’s pose in the scene.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var worldTransform: simd_float4x4 { get set }DiscussionThe value of this property requires orthogonal basis vectors and uniform scale.The framework interprets the transform’s position values in a right-handed coordinate system, where the Y axis extends upward and and the negative Z axis extends forward.See AlsoDefining a Posevar transform: simd_float4x4A matrix, in local coordinates, that determines the object’s pose in the scene.

## PHASEOccluder | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseoccluder

PHASE  PHASEOccluder ClassPHASEOccluderAn object with a shape and position that blocks audio from reaching the listener.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEOccluder Mentioned in  Playing sound from a location in a 3D scene OverviewThe framework lowers the volume of an audio signal when an instance of this class positions somewhere along the path between the sound source and the listener.For an example that demonstrates sound occlusion, see Playing sound from a location in a 3D scene.TopicsCreating an Occluderinit(engine: PHASEEngine, shapes: [PHASEShape])Creates an occluder with the given engine and shapes.Inspecting the Shapevar shapes: [PHASEShape]An array of shapes that collectively define the occluder’s audio-deflecting surface and texture.RelationshipsInherits FromPHASEObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSCopyingNSObjectProtocolSee AlsoSoundscape Creationclass PHASESourceAn object that plays audio from a 3D location and orientation in a scene.class PHASEListenerA central point of reference that defines the location within the scene that’s most audible to the user.class PHASEObjectAn object in the scene.class PHASEShapeA collection of points that connect to form a 3D volume.class ElementAn object that describes the characteristics of a physical surface.class PHASEMaterialSurface characteristics that determine the acoustic properties of an object.enum PHASEMaterialPresetA collection of physical surfaces that each add a unique acoustic quality to your app’s audio.class PHASEMixerParametersAn object that specifies a mixer for sound events and orients them in 3D space.

### init(engine:shapes:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseoccluder/init(engine:shapes:)

PHASE  PHASEOccluder  init(engine:shapes:) Initializerinit(engine:shapes:)Creates an occluder with the given engine and shapes.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    engine: PHASEEngine,
    shapes: [PHASEShape]
) Parameters engineThe object that controls the app’s audio output.shapesA collection of shapes that defines the occluder’s overall shape.

### shapes | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseoccluder/shapes

PHASE  PHASEOccluder  shapes Instance PropertyshapesAn array of shapes that collectively define the occluder’s audio-deflecting surface and texture.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var shapes: [PHASEShape] { get }DiscussionThe framework sets the contents to the shapes argument of the init(engine:shapes:) initializer.

## PHASEPlaybackMode | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseplaybackmode

PHASE  PHASEPlaybackMode EnumerationPHASEPlaybackModeLoop options for audio playback.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum PHASEPlaybackModeOverviewThis class defines the options for a sampler node’s playbackMode. These options control whether the node’s sound event automatically plays back its audio asset from the beginning after finishing.TopicsPlayback Modescase oneShotAn option that plays a sound only once.case loopingAn option that restarts a sound from the begining after it finishes.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoAudio-Providing Nodesclass PHASESamplerNodeDefinitionA node that plays complete audio data.class PHASEPushStreamNodeDefinitionA node that plays a sequence of audio buffers.class PHASEPushStreamNodeAn audio stream you manage to provide a sound buffer data.struct PHASEPushStreamBufferOptionsOptions that inform PHASE of an audio-stream buffer’s playback priority.enum PHASECalibrationModeCalibration options for sound pressure level.class PHASEGeneratorNodeDefinitionA base class for nodes that provide audio data to generate sound.

### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseplaybackmode/init(rawvalue:)

PHASE  PHASEPlaybackMode  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

### PHASEPlaybackMode.looping | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseplaybackmode/looping

PHASE  PHASEPlaybackMode  PHASEPlaybackMode.looping CasePHASEPlaybackMode.loopingAn option that restarts a sound from the begining after it finishes.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case loopingSee AlsoPlayback Modescase oneShotAn option that plays a sound only once.

### PHASEPlaybackMode.oneShot | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseplaybackmode/oneshot

PHASE  PHASEPlaybackMode  PHASEPlaybackMode.oneShot CasePHASEPlaybackMode.oneShotAn option that plays a sound only once.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case oneShotSee AlsoPlayback Modescase loopingAn option that restarts a sound from the begining after it finishes.

## PHASEPullStreamNode | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepullstreamnode

PHASE  PHASEPullStreamNode ClassPHASEPullStreamNodeiOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 2.0+class PHASEPullStreamNodeOverviewAn object for addessing an instance of a stream in an executing sound eventTopicsInstance Propertiesvar renderHandler: PHASEPullStreamRenderHandlerRelationshipsInherits FromPHASEStreamNodeConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocol

### renderHandler | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepullstreamnode/renderhandler

PHASE  PHASEPullStreamNode  renderHandler Instance PropertyrenderHandleriOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 2.0+var renderHandler: PHASEPullStreamRenderHandler { get set }DiscussionA property to set the render block callback that will render the samplesIWThe renderBlock must be set before the PHASESoundEvent is prepared or started.  The callback will be called from a high priority realtime thread. Your implementation must be performant and not perform any realtime unsafe operations such as lock mutexes or allocate memory.

## PHASEPullStreamNodeDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepullstreamnodedefinition

PHASE  PHASEPullStreamNodeDefinition ClassPHASEPullStreamNodeDefinitioniOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 2.0+class PHASEPullStreamNodeDefinitionOverviewAn object for defining a pull stream sound event node when building a sound event.TopicsInitializersinit(mixerDefinition: PHASEMixerDefinition, format: AVAudioFormat)convenience init(mixerDefinition: PHASEMixerDefinition, format: AVAudioFormat, identifier: String)Instance Propertiesvar format: AVAudioFormatvar normalize: BoolRelationshipsInherits FromPHASEGeneratorNodeDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocol

### format | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepullstreamnodedefinition/format

PHASE  PHASEPullStreamNodeDefinition  format Instance PropertyformatiOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 2.0+var format: AVAudioFormat { get }DiscussionThe readonly property that returns the AVAudioFormat that this stream was initialized with

### init(mixerDefinition:format:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepullstreamnodedefinition/init(mixerdefinition:format:)

PHASE  PHASEPullStreamNodeDefinition  init(mixerDefinition:format:) Initializerinit(mixerDefinition:format:)iOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 2.0+init(
    mixerDefinition: PHASEMixerDefinition,
    format: AVAudioFormat
) Parameters mixerDefinitionThe mixer definition this stream will be assigned toformatThe AVAudioFormat object that will define the attributes of the audio this node will accept. Only Core Audio’s standard deinterleaved 32-bit floating-point formats are supported.Return ValueA new PHASEPullStreamNodeDefinition objectDiscussionCreate a pull stream node definition

### init(mixerDefinition:format:identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepullstreamnodedefinition/init(mixerdefinition:format:identifier:)

PHASE  PHASEPullStreamNodeDefinition  init(mixerDefinition:format:identifier:) Initializerinit(mixerDefinition:format:identifier:)iOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 2.0+convenience init(
    mixerDefinition: PHASEMixerDefinition,
    format: AVAudioFormat,
    identifier: String
) Parameters mixerDefinitionThe mixer definition this stream will be assigned toformatThe AVAudioFormat object that will define the attributes of the audio this node will accept. Only Core Audio’s standard deinterleaved 32-bit floating-point formats are supported.identifierAn optional custom identifier to give to this objectReturn ValueA new PHASEPullStreamNodeDefinition objectDiscussionCreate a pull stream node definition

### normalize | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepullstreamnodedefinition/normalize

PHASE  PHASEPullStreamNodeDefinition  normalize Instance PropertynormalizeiOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 2.0+var normalize: Bool { get set }DiscussionDetermines whether or not the engine should normalize the stream. The default value is NO.In general, clients are advised to normalize the input. Normalization is required to properly calibrate the output level. If you set this value to NO, it’s advised that you do custom normalization of the audio data prior to passing the buffers to PHASE.

## PHASEPullStreamRenderHandler | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepullstreamrenderhandler

PHASE  PHASEPullStreamRenderHandler Type AliasPHASEPullStreamRenderHandleriOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+typealias PHASEPullStreamRenderHandler = (UnsafeMutablePointer<ObjCBool>, UnsafePointer<AudioTimeStamp>, AVAudioFrameCount, UnsafeMutablePointer<AudioBufferList>) -> OSStatus Parameters isSilenceThe client may use this flag to indicate that the buffer it vends contains only silence. The receiver of the buffer can then use the flag as a hint as to whether the buffer needs to be processed or not. Note that because the flag is only a hint, when setting the silence flag, the originator of a buffer must also ensure that it contains silence (zeroes).timestampThe HAL time at which the audio data will be rendered. If there is a sample rate conversion or time compression/expansion downstream, the sample time will not be valid.frameCountThe number of sample frames of audio data requested.outputDataThe output data.Return ValueAn OSStatus result code. If an error is returned, the audio data should be assumed to be invalid.DiscussionBlock to supply audio data to PHASEPullStreamNodeThe caller must supply valid buffers in outputData's mBuffers' mData and mDataByteSize.
mDataByteSize must be consistent with frameCount. This block may provide output in those
specified buffers, or it may replace the mData pointers with pointers to memory which it
owns and guarantees will remain valid until the next render cycle.

## PHASEPushStreamBufferOptions | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreambufferoptions

PHASE  PHASEPushStreamBufferOptions StructurePHASEPushStreamBufferOptionsOptions that inform PHASE of an audio-stream buffer’s playback priority.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+struct PHASEPushStreamBufferOptionsOverviewWhen your app provides audio buffers that PHASE plays through a PHASEPushStreamNode, use this structure to inform PHASE of a particular buffer’s priority.Associate an option to a particular buffer by passing it in to the scheduleBuffer(buffer:time:options:) function of a PHASEPushStreamNode.TopicsCreating an Optioninit(rawValue: UInt)Creates a push stream buffer option with the given raw value.Optionsstatic var `default`: PHASEPushStreamBufferOptionsIndicates a buffer processes after existing buffers in the queue.static var interrupts: PHASEPushStreamBufferOptionsIndicates a buffer begins processing immediately.static var interruptsAtLoop: PHASEPushStreamBufferOptionsIndicates a buffer begins processing when an existing buffer loops.static var loops: PHASEPushStreamBufferOptionsIndicates a buffer restarts after it finishes processing.RelationshipsConforms ToBitwiseCopyableEquatableExpressibleByArrayLiteralOptionSetRawRepresentableSendableSendableMetatypeSetAlgebraSee AlsoAudio-Providing Nodesclass PHASESamplerNodeDefinitionA node that plays complete audio data.enum PHASEPlaybackModeLoop options for audio playback.class PHASEPushStreamNodeDefinitionA node that plays a sequence of audio buffers.class PHASEPushStreamNodeAn audio stream you manage to provide a sound buffer data.enum PHASECalibrationModeCalibration options for sound pressure level.class PHASEGeneratorNodeDefinitionA base class for nodes that provide audio data to generate sound.

### default | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreambufferoptions/default

PHASE  PHASEPushStreamBufferOptions  default Type PropertydefaultIndicates a buffer processes after existing buffers in the queue.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var `default`: PHASEPushStreamBufferOptions { get }See AlsoOptionsstatic var interrupts: PHASEPushStreamBufferOptionsIndicates a buffer begins processing immediately.static var interruptsAtLoop: PHASEPushStreamBufferOptionsIndicates a buffer begins processing when an existing buffer loops.static var loops: PHASEPushStreamBufferOptionsIndicates a buffer restarts after it finishes processing.

### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreambufferoptions/init(rawvalue:)

PHASE  PHASEPushStreamBufferOptions  init(rawValue:) Initializerinit(rawValue:)Creates a push stream buffer option with the given raw value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init(rawValue: UInt) Parameters rawValueA raw value for the option’s enumeration case.

### interrupts | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreambufferoptions/interrupts

PHASE  PHASEPushStreamBufferOptions  interrupts Type PropertyinterruptsIndicates a buffer begins processing immediately.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var interrupts: PHASEPushStreamBufferOptions { get }See AlsoOptionsstatic var `default`: PHASEPushStreamBufferOptionsIndicates a buffer processes after existing buffers in the queue.static var interruptsAtLoop: PHASEPushStreamBufferOptionsIndicates a buffer begins processing when an existing buffer loops.static var loops: PHASEPushStreamBufferOptionsIndicates a buffer restarts after it finishes processing.

### interruptsAtLoop | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreambufferoptions/interruptsatloop

PHASE  PHASEPushStreamBufferOptions  interruptsAtLoop Type PropertyinterruptsAtLoopIndicates a buffer begins processing when an existing buffer loops.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var interruptsAtLoop: PHASEPushStreamBufferOptions { get }See AlsoOptionsstatic var `default`: PHASEPushStreamBufferOptionsIndicates a buffer processes after existing buffers in the queue.static var interrupts: PHASEPushStreamBufferOptionsIndicates a buffer begins processing immediately.static var loops: PHASEPushStreamBufferOptionsIndicates a buffer restarts after it finishes processing.

### loops | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreambufferoptions/loops

PHASE  PHASEPushStreamBufferOptions  loops Type PropertyloopsIndicates a buffer restarts after it finishes processing.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var loops: PHASEPushStreamBufferOptions { get }See AlsoOptionsstatic var `default`: PHASEPushStreamBufferOptionsIndicates a buffer processes after existing buffers in the queue.static var interrupts: PHASEPushStreamBufferOptionsIndicates a buffer begins processing immediately.static var interruptsAtLoop: PHASEPushStreamBufferOptionsIndicates a buffer begins processing when an existing buffer loops.

## PHASEPushStreamCompletionCallbackCondition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamcompletioncallbackcondition

PHASE  PHASEPushStreamCompletionCallbackCondition EnumerationPHASEPushStreamCompletionCallbackConditionA status that describes the results after the app schedules a push-stream buffer.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum PHASEPushStreamCompletionCallbackConditionOverviewA PHASEPushStreamNode object provides an instance of this class to the completion closure after the app schedules a buffer by calling scheduleBuffer(buffer:completionCallbackType:completionHandler:).TopicsConditionscase dataRenderedIndicates the framework invokes the callback when the engine processes the audio for output.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoProviding Audio Datafunc scheduleBuffer(buffer: AVAudioPCMBuffer)Schedules audio data for playback.func scheduleBuffer(buffer: AVAudioPCMBuffer, time: AVAudioTime?, options: PHASEPushStreamBufferOptions)Schedules audio data playback at a specific time.func scheduleBuffer(buffer: AVAudioPCMBuffer, time: AVAudioTime?, options: PHASEPushStreamBufferOptions, completionCallbackType: PHASEPushStreamCompletionCallbackCondition, completionHandler: (PHASEPushStreamCompletionCallbackCondition) -> Void)Schedules audio data playback at a specific time with a completion handler.func scheduleBuffer(buffer: AVAudioPCMBuffer, completionCallbackType: PHASEPushStreamCompletionCallbackCondition, completionHandler: (PHASEPushStreamCompletionCallbackCondition) -> Void)Schedules audio data playback with a completion handler.

### PHASEPushStreamCompletionCallbackCondition.dataRendered | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamcompletioncallbackcondition/datarendered

PHASE  PHASEPushStreamCompletionCallbackCondition  PHASEPushStreamCompletionCallbackCondition.dataRendered CasePHASEPushStreamCompletionCallbackCondition.dataRenderedIndicates the framework invokes the callback when the engine processes the audio for output.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case dataRendered

### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamcompletioncallbackcondition/init(rawvalue:)

PHASE  PHASEPushStreamCompletionCallbackCondition  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

## PHASEPushStreamNode | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamnode

PHASE  PHASEPushStreamNode ClassPHASEPushStreamNodeAn audio stream you manage to provide a sound buffer data.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEPushStreamNodeOverviewA sound event’s pushStreamNodes dictionary populates with an instance of this class when PHASE invokes a  PHASEPushStreamNodeDefinition in your event node tree.Your app provides the audio data that the sound event plays by calling one or more of this class’s buffer-scheduling functions, for example, scheduleBuffer(buffer:).TopicsInspecting Stream Propertiesvar mixer: PHASEMixerThe audio stream’s output pipeline.var format: AVAudioFormatThe format of the audio stream data.Providing Audio Datafunc scheduleBuffer(buffer: AVAudioPCMBuffer)Schedules audio data for playback.func scheduleBuffer(buffer: AVAudioPCMBuffer, time: AVAudioTime?, options: PHASEPushStreamBufferOptions)Schedules audio data playback at a specific time.func scheduleBuffer(buffer: AVAudioPCMBuffer, time: AVAudioTime?, options: PHASEPushStreamBufferOptions, completionCallbackType: PHASEPushStreamCompletionCallbackCondition, completionHandler: (PHASEPushStreamCompletionCallbackCondition) -> Void)Schedules audio data playback at a specific time with a completion handler.func scheduleBuffer(buffer: AVAudioPCMBuffer, completionCallbackType: PHASEPushStreamCompletionCallbackCondition, completionHandler: (PHASEPushStreamCompletionCallbackCondition) -> Void)Schedules audio data playback with a completion handler.enum PHASEPushStreamCompletionCallbackConditionA status that describes the results after the app schedules a push-stream buffer.Controlling Playbackvar gainMetaParameter: PHASENumberMetaParameter?A meta parameter for dynamic loudness control.var rateMetaParameter: PHASENumberMetaParameter?A meta parameter for dynamic rate control.RelationshipsInherits FromPHASEStreamNodeConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoAudio-Providing Nodesclass PHASESamplerNodeDefinitionA node that plays complete audio data.enum PHASEPlaybackModeLoop options for audio playback.class PHASEPushStreamNodeDefinitionA node that plays a sequence of audio buffers.struct PHASEPushStreamBufferOptionsOptions that inform PHASE of an audio-stream buffer’s playback priority.enum PHASECalibrationModeCalibration options for sound pressure level.class PHASEGeneratorNodeDefinitionA base class for nodes that provide audio data to generate sound.

### format | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamnode/format

PHASE  PHASEPushStreamNode  format Instance PropertyformatThe format of the audio stream data.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var format: AVAudioFormat { get }DiscussionThe framework sets the value to the init(mixerDefinition:format:) argument.See AlsoInspecting Stream Propertiesvar mixer: PHASEMixerThe audio stream’s output pipeline.

### gainMetaParameter | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamnode/gainmetaparameter

PHASE  PHASEPushStreamNode  gainMetaParameter Instance PropertygainMetaParameterA meta parameter for dynamic loudness control.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var gainMetaParameter: PHASENumberMetaParameter? { get }DiscussionThe framework sets this property when the app specifies a meta parameter definition at initialization.See AlsoControlling Playbackvar rateMetaParameter: PHASENumberMetaParameter?A meta parameter for dynamic rate control.

### mixer | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamnode/mixer

PHASE  PHASEPushStreamNode  mixer Instance PropertymixerThe audio stream’s output pipeline.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var mixer: PHASEMixer { get }DiscussionThe framework sets the value based on the definition initializer’s mixerDefinition argument. See init(mixerDefinition:format:).See AlsoInspecting Stream Propertiesvar format: AVAudioFormatThe format of the audio stream data.

### rateMetaParameter | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamnode/ratemetaparameter

PHASE  PHASEPushStreamNode  rateMetaParameter Instance PropertyrateMetaParameterA meta parameter for dynamic rate control.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var rateMetaParameter: PHASENumberMetaParameter? { get }DiscussionThe framework sets this property when the app specifies a meta parameter definition at initialization.See AlsoControlling Playbackvar gainMetaParameter: PHASENumberMetaParameter?A meta parameter for dynamic loudness control.

### scheduleBuffer(buffer:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamnode/schedulebuffer(buffer:)

PHASE  PHASEPushStreamNode  scheduleBuffer(buffer:) Instance MethodscheduleBuffer(buffer:)Schedules audio data for playback.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func scheduleBuffer(buffer: AVAudioPCMBuffer) Parameters bufferData that represents one portion of a contiguous audio stream.DiscussionThe framework processes this buffer after completing previously scheduled buffers. The buffer’s data format needs to match format.See AlsoProviding Audio Datafunc scheduleBuffer(buffer: AVAudioPCMBuffer, time: AVAudioTime?, options: PHASEPushStreamBufferOptions)Schedules audio data playback at a specific time.func scheduleBuffer(buffer: AVAudioPCMBuffer, time: AVAudioTime?, options: PHASEPushStreamBufferOptions, completionCallbackType: PHASEPushStreamCompletionCallbackCondition, completionHandler: (PHASEPushStreamCompletionCallbackCondition) -> Void)Schedules audio data playback at a specific time with a completion handler.func scheduleBuffer(buffer: AVAudioPCMBuffer, completionCallbackType: PHASEPushStreamCompletionCallbackCondition, completionHandler: (PHASEPushStreamCompletionCallbackCondition) -> Void)Schedules audio data playback with a completion handler.enum PHASEPushStreamCompletionCallbackConditionA status that describes the results after the app schedules a push-stream buffer.

### scheduleBuffer(buffer:completionCallbackType:completionHandler:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamnode/schedulebuffer(buffer:completioncallbacktype:completionhandler:)

PHASE  PHASEPushStreamNode  scheduleBuffer(buffer:completionCallbackType:completionHandler:) Instance MethodscheduleBuffer(buffer:completionCallbackType:completionHandler:)Schedules audio data playback with a completion handler.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func scheduleBuffer(
    buffer: AVAudioPCMBuffer,
    completionCallbackType: PHASEPushStreamCompletionCallbackCondition,
    completionHandler: @escaping (PHASEPushStreamCompletionCallbackCondition) -> Void
)func scheduleBuffer(
    buffer: AVAudioPCMBuffer,
    completionCallbackType: PHASEPushStreamCompletionCallbackCondition
) async -> PHASEPushStreamCompletionCallbackCondition Parameters bufferData that represents one portion of a contiguous audio stream.completionCallbackTypeThe specific event on which to handle completion.completionHandlerCode the framework runs on completion or when the player stops.DiscussionImportant You can call this method from synchronous code using a completion handler, as shown on this page, or you can call it as an asynchronous method that has the following declaration:func scheduleBuffer(buffer: AVAudioPCMBuffer, completionCallbackType: PHASEPushStreamCompletionCallbackCondition) async -> PHASEPushStreamCompletionCallbackCondition
For information about concurrency and asynchronous code in Swift, see Calling Objective-C APIs Asynchronously.See AlsoProviding Audio Datafunc scheduleBuffer(buffer: AVAudioPCMBuffer)Schedules audio data for playback.func scheduleBuffer(buffer: AVAudioPCMBuffer, time: AVAudioTime?, options: PHASEPushStreamBufferOptions)Schedules audio data playback at a specific time.func scheduleBuffer(buffer: AVAudioPCMBuffer, time: AVAudioTime?, options: PHASEPushStreamBufferOptions, completionCallbackType: PHASEPushStreamCompletionCallbackCondition, completionHandler: (PHASEPushStreamCompletionCallbackCondition) -> Void)Schedules audio data playback at a specific time with a completion handler.enum PHASEPushStreamCompletionCallbackConditionA status that describes the results after the app schedules a push-stream buffer.

### scheduleBuffer(buffer:time:options:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamnode/schedulebuffer(buffer:time:options:)

PHASE  PHASEPushStreamNode  scheduleBuffer(buffer:time:options:) Instance MethodscheduleBuffer(buffer:time:options:)Schedules audio data playback at a specific time.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func scheduleBuffer(
    buffer: AVAudioPCMBuffer,
    time when: AVAudioTime?,
    options: PHASEPushStreamBufferOptions = []
) Parameters bufferData that represents one portion of a contiguous audio stream.whenThe time to play the buffer.optionsThe options for looping and buffer interruption.See AlsoProviding Audio Datafunc scheduleBuffer(buffer: AVAudioPCMBuffer)Schedules audio data for playback.func scheduleBuffer(buffer: AVAudioPCMBuffer, time: AVAudioTime?, options: PHASEPushStreamBufferOptions, completionCallbackType: PHASEPushStreamCompletionCallbackCondition, completionHandler: (PHASEPushStreamCompletionCallbackCondition) -> Void)Schedules audio data playback at a specific time with a completion handler.func scheduleBuffer(buffer: AVAudioPCMBuffer, completionCallbackType: PHASEPushStreamCompletionCallbackCondition, completionHandler: (PHASEPushStreamCompletionCallbackCondition) -> Void)Schedules audio data playback with a completion handler.enum PHASEPushStreamCompletionCallbackConditionA status that describes the results after the app schedules a push-stream buffer.

### scheduleBuffer(buffer:time:options:completionCallbackType:completionHandler:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamnode/schedulebuffer(buffer:time:options:completioncallbacktype:completionhandler:)

PHASE  PHASEPushStreamNode  scheduleBuffer(buffer:time:options:completionCallbackType:completionHandler:) Instance MethodscheduleBuffer(buffer:time:options:completionCallbackType:completionHandler:)Schedules audio data playback at a specific time with a completion handler.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func scheduleBuffer(
    buffer: AVAudioPCMBuffer,
    time when: AVAudioTime?,
    options: PHASEPushStreamBufferOptions = [],
    completionCallbackType: PHASEPushStreamCompletionCallbackCondition,
    completionHandler: @escaping (PHASEPushStreamCompletionCallbackCondition) -> Void
)func scheduleBuffer(
    buffer: AVAudioPCMBuffer,
    time when: AVAudioTime?,
    options: PHASEPushStreamBufferOptions = [],
    completionCallbackType: PHASEPushStreamCompletionCallbackCondition
) async -> PHASEPushStreamCompletionCallbackCondition Parameters bufferData that represents one portion of a contiguous audio stream.whenThe time to play the buffer.optionsThe options for looping and buffer interruption.completionCallbackTypeThe specific event on which to handle completion.completionHandlerCode the framework runs on completion or when the player stops.DiscussionImportant You can call this method from synchronous code using a completion handler, as shown on this page, or you can call it as an asynchronous method that has the following declaration:func scheduleBuffer(buffer: AVAudioPCMBuffer, time when: AVAudioTime?, options: PHASEPushStreamBufferOptions = [], completionCallbackType: PHASEPushStreamCompletionCallbackCondition) async -> PHASEPushStreamCompletionCallbackCondition
For information about concurrency and asynchronous code in Swift, see Calling Objective-C APIs Asynchronously.See AlsoProviding Audio Datafunc scheduleBuffer(buffer: AVAudioPCMBuffer)Schedules audio data for playback.func scheduleBuffer(buffer: AVAudioPCMBuffer, time: AVAudioTime?, options: PHASEPushStreamBufferOptions)Schedules audio data playback at a specific time.func scheduleBuffer(buffer: AVAudioPCMBuffer, completionCallbackType: PHASEPushStreamCompletionCallbackCondition, completionHandler: (PHASEPushStreamCompletionCallbackCondition) -> Void)Schedules audio data playback with a completion handler.enum PHASEPushStreamCompletionCallbackConditionA status that describes the results after the app schedules a push-stream buffer.

## PHASEPushStreamNodeDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamnodedefinition

PHASE  PHASEPushStreamNodeDefinition ClassPHASEPushStreamNodeDefinitionA node that plays a sequence of audio buffers.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEPushStreamNodeDefinitionOverviewUse this node to create sound events for a piecemeal audio source, for example, an audio stream that your app accesses over the network or loads from a memory-mapped file on disk.Note To create a sound event for fully-loaded audio data instead, use PHASESamplerNodeDefinition.TopicsCreating a Nodeinit(mixerDefinition: PHASEMixerDefinition, format: AVAudioFormat)Creates a node definition for audio streams.convenience init(mixerDefinition: PHASEMixerDefinition, format: AVAudioFormat, identifier: String)Creates a named node definition for audio streams.Observing the Formatvar format: AVAudioFormatThe format of the audio stream data.Shaping Loudnessvar normalize: BoolAn option that resizes loudness of the audio stream for consistency.RelationshipsInherits FromPHASEGeneratorNodeDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoAudio-Providing Nodesclass PHASESamplerNodeDefinitionA node that plays complete audio data.enum PHASEPlaybackModeLoop options for audio playback.class PHASEPushStreamNodeAn audio stream you manage to provide a sound buffer data.struct PHASEPushStreamBufferOptionsOptions that inform PHASE of an audio-stream buffer’s playback priority.enum PHASECalibrationModeCalibration options for sound pressure level.class PHASEGeneratorNodeDefinitionA base class for nodes that provide audio data to generate sound.

### format | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamnodedefinition/format

PHASE  PHASEPushStreamNodeDefinition  format Instance PropertyformatThe format of the audio stream data.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var format: AVAudioFormat { get }

### init(mixerDefinition:format:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamnodedefinition/init(mixerdefinition:format:)

PHASE  PHASEPushStreamNodeDefinition  init(mixerDefinition:format:) Initializerinit(mixerDefinition:format:)Creates a node definition for audio streams.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    mixerDefinition: PHASEMixerDefinition,
    format: AVAudioFormat
) Parameters mixerDefinitionAn object that combines audio layers.formatThe format of the audio stream data.See AlsoCreating a Nodeconvenience init(mixerDefinition: PHASEMixerDefinition, format: AVAudioFormat, identifier: String)Creates a named node definition for audio streams.

### init(mixerDefinition:format:identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamnodedefinition/init(mixerdefinition:format:identifier:)

PHASE  PHASEPushStreamNodeDefinition  init(mixerDefinition:format:identifier:) Initializerinit(mixerDefinition:format:identifier:)Creates a named node definition for audio streams.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+convenience init(
    mixerDefinition: PHASEMixerDefinition,
    format: AVAudioFormat,
    identifier: String
) Parameters mixerDefinitionAn object that combines audio layers.formatThe format of the audio stream data.identifierA unique name for the node.See AlsoCreating a Nodeinit(mixerDefinition: PHASEMixerDefinition, format: AVAudioFormat)Creates a node definition for audio streams.

### normalize | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasepushstreamnodedefinition/normalize

PHASE  PHASEPushStreamNodeDefinition  normalize Instance PropertynormalizeAn option that resizes loudness of the audio stream for consistency.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var normalize: Bool { get set }DiscussionThe default value is false. When true, the engine normalizes the audio stream — that is, it dynamically resizes loudness within a given range for a consistent listening experience. Normalization serves the benefit of assisting output level calibration. Apps that leave the value false need to normalize stream data manually before passing it into the framework (see pushStreamNodes).

## PHASERandomNodeDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaserandomnodedefinition

PHASE  PHASERandomNodeDefinition ClassPHASERandomNodeDefinitionA sound event node that invokes one of its child nodes at random.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASERandomNodeDefinitionOverviewWhen the framework invokes a random node, it passes the invocation on to one of its children at random. The weight you choose for a child node in the addSubtree(_:weight:) argument skews the node’s selection chances.Choose from Alternate SoundsThis class can model real-world cases where an event varies slightly, such as when footsteps sound slightly different because of the unique ground composition at each step.The following code creates an instance of this class that selects from three different footstep sounds. The weights determine that an uncommon footstep noise plays half as frequently as the common footstep. And a third footstep noise plays 10% of the time.// Create several nodes from prior-registered footstep sound assets.
let footstep1 = PHASESamplerNodeDefinition(
    soundAssetIdentifier: "footstep1",
    mixerDefinition: myMixer, identifier: "footstep1")
let footstep2 = PHASESamplerNodeDefinition(
    soundAssetIdentifier: "footstep2",
    mixerDefinition: myMixer, identifier: "footstep2")
let footstep3 = PHASESamplerNodeDefinition(
    soundAssetIdentifier: "footstep3",    
    mixerDefinition: myMixer, identifier: "footstep3")

// Create the random node.
let randomNode = PHASERandomNodeDefinition(identifier: "randomNode")

// Connect leaf nodes to the tree and set the weights. 
randomNode.addSubtree(footstep1, weight: 10)
randomNode.addSubtree(footstep2, weight: 5)
randomNode.addSubtree(footstep3, weight: 1)
// Create several nodes from prior-registered footstep sound assets.
PHASESamplerNodeDefinition* footstep1 = 
    [[PHASESamplerNodeDefinition alloc] 
        initWithSoundAssetUID:@"footstep1" 
        mixerDefinition:mixNode uid:@"footstep1"];
PHASESamplerNodeDefinition* footstep2 = 
    [[PHASESamplerNodeDefinition alloc] 
        initWithSoundAssetUID:@"footstep2" 
        mixerDefinition:mixNode uid:@"footstep2"];
PHASESamplerNodeDefinition* footstep3 = 
    [[PHASESamplerNodeDefinition alloc] 
        initWithSoundAssetUID:@"footstep3" 
        mixerDefinition:mixNode uid:@"footstep3"];

// Create the random node.
PHASERandomNodeDefinition* randomNode = 
    [[PHASERandomNodeDefinition alloc] initWithUID:@"randomNode"];

// Connect leaf nodes to the tree and set the weights. 
[randomNode addSubtree:footstep1 weight:@10];
[randomNode addSubtree:footstep2 weight:@5];
[randomNode addSubtree:footstep3 weight:@1];
TopicsCreating a Nodeinit()Creates a random node.convenience init(identifier: String)Creates a random node with the name you specify.Adding Descendent Nodesfunc addSubtree(PHASESoundEventNodeDefinition, weight: NSNumber)Adds a node tree that’s one of the random-selection options.Defining Selection Queue Lengthvar uniqueSelectionQueueLength: IntThe length of the unique selection queue.RelationshipsInherits FromPHASESoundEventNodeDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoControl Nodesclass PHASESwitchNodeDefinitionA node that passes invocation to only one of its child nodes.class PHASEBlendNodeDefinitionA node that smoothly fades between the audio of its child nodes.class PHASEContainerNodeDefinitionA node that plays all its children at the same time.

### addSubtree(_:weight:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaserandomnodedefinition/addsubtree(_:weight:)

PHASE  PHASERandomNodeDefinition  addSubtree(_:weight:) Instance MethodaddSubtree(_:weight:)Adds a node tree that’s one of the random-selection options.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func addSubtree(
    _ subtree: PHASESoundEventNodeDefinition,
    weight: NSNumber
) Parameters subtreeThe child node, which itself can contain a hierarchical tree of descendent nodes.weightA number that implements favoritism in the random selection.

### init() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaserandomnodedefinition/init()

PHASE  PHASERandomNodeDefinition  init() Initializerinit()Creates a random node.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init()See AlsoCreating a Nodeconvenience init(identifier: String)Creates a random node with the name you specify.

### init(identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaserandomnodedefinition/init(identifier:)

PHASE  PHASERandomNodeDefinition  init(identifier:) Initializerinit(identifier:)Creates a random node with the name you specify.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+convenience init(identifier: String) Parameters identifierA unique name for the node.See AlsoCreating a Nodeinit()Creates a random node.

### uniqueSelectionQueueLength | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaserandomnodedefinition/uniqueselectionqueuelength

PHASE  PHASERandomNodeDefinition  uniqueSelectionQueueLength Instance PropertyuniqueSelectionQueueLengthThe length of the unique selection queue.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var uniqueSelectionQueueLength: Int { get set }

## PHASEReverbPreset | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasereverbpreset

PHASE  PHASEReverbPreset EnumerationPHASEReverbPresetThe manner in which PHASE diffuses resonating sound.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum PHASEReverbPresetOverviewThe PHASE engine requires your app to choose an option of this enumeration and assign it to the defaultReverbPreset property.The value you choose adds resonation to sound that simulates the experience of hearing it in a particular environment. For example, a small room, PHASEReverbPreset.smallRoom, adds very little reverberation compared to a large chamber, PHASEReverbPreset.largeChamber.TopicsPresetscase cathedralA resonation that simulates the experience of hearing a sound in a cathedral.case largeChamberA resonation that simulates the experience of hearing a sound in a large chamber with specific dimensions.case largeHallA resonation that simulates the experience of hearing a sound in a large hall with specific dimensions.case largeHall2A resonation that simulates the experience of hearing a sound in one kind of large hall with specific dimensions.case largeRoomA resonation that simulates the experience of hearing a sound in a large room with specific dimensions.case largeRoom2A resonation that simulates the experience of hearing a sound in one kind of large room with specific dimensions.case mediumChamberA resonation that simulates the experience of hearing a sound in a medium-size chamber with specific dimensions.case mediumHallA resonation that simulates the experience of hearing a sound in a medium-size hall with specific dimensions.case mediumHall2A resonation that simulates the experience of hearing a sound in one kind of medium-size hall with specific dimensions.case mediumHall3A resonation that simulates the experience of hearing a sound in another kind of medium-size hall with specific dimensions.case mediumRoomA resonation that simulates the experience of hearing a sound in a medium-size room with specific dimensions.case noneAn option that adds no reverberation to a sound.case smallRoomA resonation that simulates the experience of hearing a sound in a small room with specific dimensions.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoSetupclass PHASEEngineAn object that manages audio assets, controls playback, and configures environmental effects.enum UpdateModeModes that determine when the framework consumes API calls and updates internal state.enum RenderingModeModes that determine whether the system renders audio in process or out of process.Betaclass PHASEAssetRegistryA central repository of audio assets.enum PHASENormalizationModeOptions that determine whether the framework adjusts a sound asset’s loudness for the user’s output device.enum PHASESpatializationModeThe manner in which PHASE outputs spatial audio.class PHASEMediumA property or quality of the environment that affects how sound travels.

### PHASEReverbPreset.cathedral | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasereverbpreset/cathedral

PHASE  PHASEReverbPreset  PHASEReverbPreset.cathedral CasePHASEReverbPreset.cathedralA resonation that simulates the experience of hearing a sound in a cathedral.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case cathedralSee AlsoPresetscase largeChamberA resonation that simulates the experience of hearing a sound in a large chamber with specific dimensions.case largeHallA resonation that simulates the experience of hearing a sound in a large hall with specific dimensions.case largeHall2A resonation that simulates the experience of hearing a sound in one kind of large hall with specific dimensions.case largeRoomA resonation that simulates the experience of hearing a sound in a large room with specific dimensions.case largeRoom2A resonation that simulates the experience of hearing a sound in one kind of large room with specific dimensions.case mediumChamberA resonation that simulates the experience of hearing a sound in a medium-size chamber with specific dimensions.case mediumHallA resonation that simulates the experience of hearing a sound in a medium-size hall with specific dimensions.case mediumHall2A resonation that simulates the experience of hearing a sound in one kind of medium-size hall with specific dimensions.case mediumHall3A resonation that simulates the experience of hearing a sound in another kind of medium-size hall with specific dimensions.case mediumRoomA resonation that simulates the experience of hearing a sound in a medium-size room with specific dimensions.case noneAn option that adds no reverberation to a sound.case smallRoomA resonation that simulates the experience of hearing a sound in a small room with specific dimensions.

### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasereverbpreset/init(rawvalue:)

PHASE  PHASEReverbPreset  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

### PHASEReverbPreset.largeChamber | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasereverbpreset/largechamber

PHASE  PHASEReverbPreset  PHASEReverbPreset.largeChamber CasePHASEReverbPreset.largeChamberA resonation that simulates the experience of hearing a sound in a large chamber with specific dimensions.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case largeChamberSee AlsoPresetscase cathedralA resonation that simulates the experience of hearing a sound in a cathedral.case largeHallA resonation that simulates the experience of hearing a sound in a large hall with specific dimensions.case largeHall2A resonation that simulates the experience of hearing a sound in one kind of large hall with specific dimensions.case largeRoomA resonation that simulates the experience of hearing a sound in a large room with specific dimensions.case largeRoom2A resonation that simulates the experience of hearing a sound in one kind of large room with specific dimensions.case mediumChamberA resonation that simulates the experience of hearing a sound in a medium-size chamber with specific dimensions.case mediumHallA resonation that simulates the experience of hearing a sound in a medium-size hall with specific dimensions.case mediumHall2A resonation that simulates the experience of hearing a sound in one kind of medium-size hall with specific dimensions.case mediumHall3A resonation that simulates the experience of hearing a sound in another kind of medium-size hall with specific dimensions.case mediumRoomA resonation that simulates the experience of hearing a sound in a medium-size room with specific dimensions.case noneAn option that adds no reverberation to a sound.case smallRoomA resonation that simulates the experience of hearing a sound in a small room with specific dimensions.

### PHASEReverbPreset.largeHall | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasereverbpreset/largehall

PHASE  PHASEReverbPreset  PHASEReverbPreset.largeHall CasePHASEReverbPreset.largeHallA resonation that simulates the experience of hearing a sound in a large hall with specific dimensions.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case largeHallSee AlsoPresetscase cathedralA resonation that simulates the experience of hearing a sound in a cathedral.case largeChamberA resonation that simulates the experience of hearing a sound in a large chamber with specific dimensions.case largeHall2A resonation that simulates the experience of hearing a sound in one kind of large hall with specific dimensions.case largeRoomA resonation that simulates the experience of hearing a sound in a large room with specific dimensions.case largeRoom2A resonation that simulates the experience of hearing a sound in one kind of large room with specific dimensions.case mediumChamberA resonation that simulates the experience of hearing a sound in a medium-size chamber with specific dimensions.case mediumHallA resonation that simulates the experience of hearing a sound in a medium-size hall with specific dimensions.case mediumHall2A resonation that simulates the experience of hearing a sound in one kind of medium-size hall with specific dimensions.case mediumHall3A resonation that simulates the experience of hearing a sound in another kind of medium-size hall with specific dimensions.case mediumRoomA resonation that simulates the experience of hearing a sound in a medium-size room with specific dimensions.case noneAn option that adds no reverberation to a sound.case smallRoomA resonation that simulates the experience of hearing a sound in a small room with specific dimensions.

### PHASEReverbPreset.largeHall2 | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasereverbpreset/largehall2

PHASE  PHASEReverbPreset  PHASEReverbPreset.largeHall2 CasePHASEReverbPreset.largeHall2A resonation that simulates the experience of hearing a sound in one kind of large hall with specific dimensions.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case largeHall2See AlsoPresetscase cathedralA resonation that simulates the experience of hearing a sound in a cathedral.case largeChamberA resonation that simulates the experience of hearing a sound in a large chamber with specific dimensions.case largeHallA resonation that simulates the experience of hearing a sound in a large hall with specific dimensions.case largeRoomA resonation that simulates the experience of hearing a sound in a large room with specific dimensions.case largeRoom2A resonation that simulates the experience of hearing a sound in one kind of large room with specific dimensions.case mediumChamberA resonation that simulates the experience of hearing a sound in a medium-size chamber with specific dimensions.case mediumHallA resonation that simulates the experience of hearing a sound in a medium-size hall with specific dimensions.case mediumHall2A resonation that simulates the experience of hearing a sound in one kind of medium-size hall with specific dimensions.case mediumHall3A resonation that simulates the experience of hearing a sound in another kind of medium-size hall with specific dimensions.case mediumRoomA resonation that simulates the experience of hearing a sound in a medium-size room with specific dimensions.case noneAn option that adds no reverberation to a sound.case smallRoomA resonation that simulates the experience of hearing a sound in a small room with specific dimensions.

### PHASEReverbPreset.largeRoom | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasereverbpreset/largeroom

PHASE  PHASEReverbPreset  PHASEReverbPreset.largeRoom CasePHASEReverbPreset.largeRoomA resonation that simulates the experience of hearing a sound in a large room with specific dimensions.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case largeRoomSee AlsoPresetscase cathedralA resonation that simulates the experience of hearing a sound in a cathedral.case largeChamberA resonation that simulates the experience of hearing a sound in a large chamber with specific dimensions.case largeHallA resonation that simulates the experience of hearing a sound in a large hall with specific dimensions.case largeHall2A resonation that simulates the experience of hearing a sound in one kind of large hall with specific dimensions.case largeRoom2A resonation that simulates the experience of hearing a sound in one kind of large room with specific dimensions.case mediumChamberA resonation that simulates the experience of hearing a sound in a medium-size chamber with specific dimensions.case mediumHallA resonation that simulates the experience of hearing a sound in a medium-size hall with specific dimensions.case mediumHall2A resonation that simulates the experience of hearing a sound in one kind of medium-size hall with specific dimensions.case mediumHall3A resonation that simulates the experience of hearing a sound in another kind of medium-size hall with specific dimensions.case mediumRoomA resonation that simulates the experience of hearing a sound in a medium-size room with specific dimensions.case noneAn option that adds no reverberation to a sound.case smallRoomA resonation that simulates the experience of hearing a sound in a small room with specific dimensions.

### PHASEReverbPreset.largeRoom2 | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasereverbpreset/largeroom2

PHASE  PHASEReverbPreset  PHASEReverbPreset.largeRoom2 CasePHASEReverbPreset.largeRoom2A resonation that simulates the experience of hearing a sound in one kind of large room with specific dimensions.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case largeRoom2See AlsoPresetscase cathedralA resonation that simulates the experience of hearing a sound in a cathedral.case largeChamberA resonation that simulates the experience of hearing a sound in a large chamber with specific dimensions.case largeHallA resonation that simulates the experience of hearing a sound in a large hall with specific dimensions.case largeHall2A resonation that simulates the experience of hearing a sound in one kind of large hall with specific dimensions.case largeRoomA resonation that simulates the experience of hearing a sound in a large room with specific dimensions.case mediumChamberA resonation that simulates the experience of hearing a sound in a medium-size chamber with specific dimensions.case mediumHallA resonation that simulates the experience of hearing a sound in a medium-size hall with specific dimensions.case mediumHall2A resonation that simulates the experience of hearing a sound in one kind of medium-size hall with specific dimensions.case mediumHall3A resonation that simulates the experience of hearing a sound in another kind of medium-size hall with specific dimensions.case mediumRoomA resonation that simulates the experience of hearing a sound in a medium-size room with specific dimensions.case noneAn option that adds no reverberation to a sound.case smallRoomA resonation that simulates the experience of hearing a sound in a small room with specific dimensions.

### PHASEReverbPreset.mediumChamber | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasereverbpreset/mediumchamber

PHASE  PHASEReverbPreset  PHASEReverbPreset.mediumChamber CasePHASEReverbPreset.mediumChamberA resonation that simulates the experience of hearing a sound in a medium-size chamber with specific dimensions.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case mediumChamberSee AlsoPresetscase cathedralA resonation that simulates the experience of hearing a sound in a cathedral.case largeChamberA resonation that simulates the experience of hearing a sound in a large chamber with specific dimensions.case largeHallA resonation that simulates the experience of hearing a sound in a large hall with specific dimensions.case largeHall2A resonation that simulates the experience of hearing a sound in one kind of large hall with specific dimensions.case largeRoomA resonation that simulates the experience of hearing a sound in a large room with specific dimensions.case largeRoom2A resonation that simulates the experience of hearing a sound in one kind of large room with specific dimensions.case mediumHallA resonation that simulates the experience of hearing a sound in a medium-size hall with specific dimensions.case mediumHall2A resonation that simulates the experience of hearing a sound in one kind of medium-size hall with specific dimensions.case mediumHall3A resonation that simulates the experience of hearing a sound in another kind of medium-size hall with specific dimensions.case mediumRoomA resonation that simulates the experience of hearing a sound in a medium-size room with specific dimensions.case noneAn option that adds no reverberation to a sound.case smallRoomA resonation that simulates the experience of hearing a sound in a small room with specific dimensions.

### PHASEReverbPreset.mediumHall | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasereverbpreset/mediumhall

PHASE  PHASEReverbPreset  PHASEReverbPreset.mediumHall CasePHASEReverbPreset.mediumHallA resonation that simulates the experience of hearing a sound in a medium-size hall with specific dimensions.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case mediumHallSee AlsoPresetscase cathedralA resonation that simulates the experience of hearing a sound in a cathedral.case largeChamberA resonation that simulates the experience of hearing a sound in a large chamber with specific dimensions.case largeHallA resonation that simulates the experience of hearing a sound in a large hall with specific dimensions.case largeHall2A resonation that simulates the experience of hearing a sound in one kind of large hall with specific dimensions.case largeRoomA resonation that simulates the experience of hearing a sound in a large room with specific dimensions.case largeRoom2A resonation that simulates the experience of hearing a sound in one kind of large room with specific dimensions.case mediumChamberA resonation that simulates the experience of hearing a sound in a medium-size chamber with specific dimensions.case mediumHall2A resonation that simulates the experience of hearing a sound in one kind of medium-size hall with specific dimensions.case mediumHall3A resonation that simulates the experience of hearing a sound in another kind of medium-size hall with specific dimensions.case mediumRoomA resonation that simulates the experience of hearing a sound in a medium-size room with specific dimensions.case noneAn option that adds no reverberation to a sound.case smallRoomA resonation that simulates the experience of hearing a sound in a small room with specific dimensions.

### PHASEReverbPreset.mediumHall2 | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasereverbpreset/mediumhall2

PHASE  PHASEReverbPreset  PHASEReverbPreset.mediumHall2 CasePHASEReverbPreset.mediumHall2A resonation that simulates the experience of hearing a sound in one kind of medium-size hall with specific dimensions.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case mediumHall2See AlsoPresetscase cathedralA resonation that simulates the experience of hearing a sound in a cathedral.case largeChamberA resonation that simulates the experience of hearing a sound in a large chamber with specific dimensions.case largeHallA resonation that simulates the experience of hearing a sound in a large hall with specific dimensions.case largeHall2A resonation that simulates the experience of hearing a sound in one kind of large hall with specific dimensions.case largeRoomA resonation that simulates the experience of hearing a sound in a large room with specific dimensions.case largeRoom2A resonation that simulates the experience of hearing a sound in one kind of large room with specific dimensions.case mediumChamberA resonation that simulates the experience of hearing a sound in a medium-size chamber with specific dimensions.case mediumHallA resonation that simulates the experience of hearing a sound in a medium-size hall with specific dimensions.case mediumHall3A resonation that simulates the experience of hearing a sound in another kind of medium-size hall with specific dimensions.case mediumRoomA resonation that simulates the experience of hearing a sound in a medium-size room with specific dimensions.case noneAn option that adds no reverberation to a sound.case smallRoomA resonation that simulates the experience of hearing a sound in a small room with specific dimensions.

### PHASEReverbPreset.mediumHall3 | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasereverbpreset/mediumhall3

PHASE  PHASEReverbPreset  PHASEReverbPreset.mediumHall3 CasePHASEReverbPreset.mediumHall3A resonation that simulates the experience of hearing a sound in another kind of medium-size hall with specific dimensions.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case mediumHall3See AlsoPresetscase cathedralA resonation that simulates the experience of hearing a sound in a cathedral.case largeChamberA resonation that simulates the experience of hearing a sound in a large chamber with specific dimensions.case largeHallA resonation that simulates the experience of hearing a sound in a large hall with specific dimensions.case largeHall2A resonation that simulates the experience of hearing a sound in one kind of large hall with specific dimensions.case largeRoomA resonation that simulates the experience of hearing a sound in a large room with specific dimensions.case largeRoom2A resonation that simulates the experience of hearing a sound in one kind of large room with specific dimensions.case mediumChamberA resonation that simulates the experience of hearing a sound in a medium-size chamber with specific dimensions.case mediumHallA resonation that simulates the experience of hearing a sound in a medium-size hall with specific dimensions.case mediumHall2A resonation that simulates the experience of hearing a sound in one kind of medium-size hall with specific dimensions.case mediumRoomA resonation that simulates the experience of hearing a sound in a medium-size room with specific dimensions.case noneAn option that adds no reverberation to a sound.case smallRoomA resonation that simulates the experience of hearing a sound in a small room with specific dimensions.

### PHASEReverbPreset.mediumRoom | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasereverbpreset/mediumroom

PHASE  PHASEReverbPreset  PHASEReverbPreset.mediumRoom CasePHASEReverbPreset.mediumRoomA resonation that simulates the experience of hearing a sound in a medium-size room with specific dimensions.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case mediumRoomSee AlsoPresetscase cathedralA resonation that simulates the experience of hearing a sound in a cathedral.case largeChamberA resonation that simulates the experience of hearing a sound in a large chamber with specific dimensions.case largeHallA resonation that simulates the experience of hearing a sound in a large hall with specific dimensions.case largeHall2A resonation that simulates the experience of hearing a sound in one kind of large hall with specific dimensions.case largeRoomA resonation that simulates the experience of hearing a sound in a large room with specific dimensions.case largeRoom2A resonation that simulates the experience of hearing a sound in one kind of large room with specific dimensions.case mediumChamberA resonation that simulates the experience of hearing a sound in a medium-size chamber with specific dimensions.case mediumHallA resonation that simulates the experience of hearing a sound in a medium-size hall with specific dimensions.case mediumHall2A resonation that simulates the experience of hearing a sound in one kind of medium-size hall with specific dimensions.case mediumHall3A resonation that simulates the experience of hearing a sound in another kind of medium-size hall with specific dimensions.case noneAn option that adds no reverberation to a sound.case smallRoomA resonation that simulates the experience of hearing a sound in a small room with specific dimensions.

### PHASEReverbPreset.none | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasereverbpreset/none

PHASE  PHASEReverbPreset  PHASEReverbPreset.none CasePHASEReverbPreset.noneAn option that adds no reverberation to a sound.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case noneSee AlsoPresetscase cathedralA resonation that simulates the experience of hearing a sound in a cathedral.case largeChamberA resonation that simulates the experience of hearing a sound in a large chamber with specific dimensions.case largeHallA resonation that simulates the experience of hearing a sound in a large hall with specific dimensions.case largeHall2A resonation that simulates the experience of hearing a sound in one kind of large hall with specific dimensions.case largeRoomA resonation that simulates the experience of hearing a sound in a large room with specific dimensions.case largeRoom2A resonation that simulates the experience of hearing a sound in one kind of large room with specific dimensions.case mediumChamberA resonation that simulates the experience of hearing a sound in a medium-size chamber with specific dimensions.case mediumHallA resonation that simulates the experience of hearing a sound in a medium-size hall with specific dimensions.case mediumHall2A resonation that simulates the experience of hearing a sound in one kind of medium-size hall with specific dimensions.case mediumHall3A resonation that simulates the experience of hearing a sound in another kind of medium-size hall with specific dimensions.case mediumRoomA resonation that simulates the experience of hearing a sound in a medium-size room with specific dimensions.case smallRoomA resonation that simulates the experience of hearing a sound in a small room with specific dimensions.

### PHASEReverbPreset.smallRoom | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasereverbpreset/smallroom

PHASE  PHASEReverbPreset  PHASEReverbPreset.smallRoom CasePHASEReverbPreset.smallRoomA resonation that simulates the experience of hearing a sound in a small room with specific dimensions.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case smallRoomSee AlsoPresetscase cathedralA resonation that simulates the experience of hearing a sound in a cathedral.case largeChamberA resonation that simulates the experience of hearing a sound in a large chamber with specific dimensions.case largeHallA resonation that simulates the experience of hearing a sound in a large hall with specific dimensions.case largeHall2A resonation that simulates the experience of hearing a sound in one kind of large hall with specific dimensions.case largeRoomA resonation that simulates the experience of hearing a sound in a large room with specific dimensions.case largeRoom2A resonation that simulates the experience of hearing a sound in one kind of large room with specific dimensions.case mediumChamberA resonation that simulates the experience of hearing a sound in a medium-size chamber with specific dimensions.case mediumHallA resonation that simulates the experience of hearing a sound in a medium-size hall with specific dimensions.case mediumHall2A resonation that simulates the experience of hearing a sound in one kind of medium-size hall with specific dimensions.case mediumHall3A resonation that simulates the experience of hearing a sound in another kind of medium-size hall with specific dimensions.case mediumRoomA resonation that simulates the experience of hearing a sound in a medium-size room with specific dimensions.case noneAn option that adds no reverberation to a sound.

## PHASESamplerNodeDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesamplernodedefinition

PHASE  PHASESamplerNodeDefinition ClassPHASESamplerNodeDefinitionA node that plays complete audio data.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASESamplerNodeDefinitionOverviewGenerate sound events from this node to play audio data that your app loads completely, either from disk or from memory.TopicsCreating a Sampler Nodeinit(soundAssetIdentifier: String, mixerDefinition: PHASEMixerDefinition)Creates a sampler node with the given sound asset and mixer.convenience init(soundAssetIdentifier: String, mixerDefinition: PHASEMixerDefinition, identifier: String)Creates a named sampler node with the given sound asset and mixer.Identifying the Audiovar assetIdentifier: StringThe name of the audio this node plays.Defining Cull Behaviorvar cullOption: PHASECullOptionThe action the engine performs after it temporarily removes the node’s sound from the audio output.enum PHASECullOptionThe actions the engine takes when it culls sound.Looping the Audiovar playbackMode: PHASEPlaybackModeAn option that determines whether the node’s audio plays in a loop.RelationshipsInherits FromPHASEGeneratorNodeDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoAudio-Providing Nodesenum PHASEPlaybackModeLoop options for audio playback.class PHASEPushStreamNodeDefinitionA node that plays a sequence of audio buffers.class PHASEPushStreamNodeAn audio stream you manage to provide a sound buffer data.struct PHASEPushStreamBufferOptionsOptions that inform PHASE of an audio-stream buffer’s playback priority.enum PHASECalibrationModeCalibration options for sound pressure level.class PHASEGeneratorNodeDefinitionA base class for nodes that provide audio data to generate sound.

### assetIdentifier | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesamplernodedefinition/assetidentifier

PHASE  PHASESamplerNodeDefinition  assetIdentifier Instance PropertyassetIdentifierThe name of the audio this node plays.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var assetIdentifier: String { get }DiscussionThis property refers to the registered identifier of the audio file. See registerSoundAsset(url:identifier:assetType:channelLayout:normalizationMode:).

### cullOption | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesamplernodedefinition/culloption

PHASE  PHASESamplerNodeDefinition  cullOption Instance PropertycullOptionThe action the engine performs after it temporarily removes the node’s sound from the audio output.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var cullOption: PHASECullOption { get set }See AlsoDefining Cull Behaviorenum PHASECullOptionThe actions the engine takes when it culls sound.

### init(soundAssetIdentifier:mixerDefinition:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesamplernodedefinition/init(soundassetidentifier:mixerdefinition:)

PHASE  PHASESamplerNodeDefinition  init(soundAssetIdentifier:mixerDefinition:) Initializerinit(soundAssetIdentifier:mixerDefinition:)Creates a sampler node with the given sound asset and mixer.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    soundAssetIdentifier: String,
    mixerDefinition: PHASEMixerDefinition
) Parameters soundAssetIdentifierA name that refers to the audio data that the node plays. See assetIdentifier.mixerDefinitionAn object that combines audio layers.See AlsoCreating a Sampler Nodeconvenience init(soundAssetIdentifier: String, mixerDefinition: PHASEMixerDefinition, identifier: String)Creates a named sampler node with the given sound asset and mixer.

### init(soundAssetIdentifier:mixerDefinition:identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesamplernodedefinition/init(soundassetidentifier:mixerdefinition:identifier:)

PHASE  PHASESamplerNodeDefinition  init(soundAssetIdentifier:mixerDefinition:identifier:) Initializerinit(soundAssetIdentifier:mixerDefinition:identifier:)Creates a named sampler node with the given sound asset and mixer.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+convenience init(
    soundAssetIdentifier: String,
    mixerDefinition: PHASEMixerDefinition,
    identifier: String
) Parameters soundAssetIdentifierA name that refers to the audio data that the node plays. See assetIdentifier.mixerDefinitionAn object that combines audio layers.identifierA unique name for the sample node.See AlsoCreating a Sampler Nodeinit(soundAssetIdentifier: String, mixerDefinition: PHASEMixerDefinition)Creates a sampler node with the given sound asset and mixer.

### playbackMode | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesamplernodedefinition/playbackmode

PHASE  PHASESamplerNodeDefinition  playbackMode Instance PropertyplaybackModeAn option that determines whether the node’s audio plays in a loop.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var playbackMode: PHASEPlaybackMode { get set }

## PHASEShape | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseshape

PHASE  PHASEShape ClassPHASEShapeA collection of points that connect to form a 3D volume.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEShape Mentioned in  Playing sound from a location in a 3D scene OverviewTo define your scene’s important 3D volumes, create one or more of the following surfaces and add them to your scene’s shapes array:The audio-emitting surface of a volumetric PHASESourceThe audio-deflecting surface and texture of a PHASEOccluderTopicsCreating a Shapeinit(engine: PHASEEngine, mesh: MDLMesh)Creates an object that the given geometric data shapes.convenience init(engine: PHASEEngine, mesh: MDLMesh, materials: [PHASEMaterial])Creates an object of a specific material that the given geometric data shapes.Describing Surface Characteristicsvar elements: [PHASEShape.Element]An array of objects that collectively describe the physical characteristics of a surface.class ElementAn object that describes the characteristics of a physical surface.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSCopyingNSObjectProtocolSee AlsoSoundscape Creationclass PHASESourceAn object that plays audio from a 3D location and orientation in a scene.class PHASEListenerA central point of reference that defines the location within the scene that’s most audible to the user.class PHASEOccluderAn object with a shape and position that blocks audio from reaching the listener.class PHASEObjectAn object in the scene.class ElementAn object that describes the characteristics of a physical surface.class PHASEMaterialSurface characteristics that determine the acoustic properties of an object.enum PHASEMaterialPresetA collection of physical surfaces that each add a unique acoustic quality to your app’s audio.class PHASEMixerParametersAn object that specifies a mixer for sound events and orients them in 3D space.

### PHASEShape.Element | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseshape/element

PHASE  PHASEShape  PHASEShape.Element ClassPHASEShape.ElementAn object that describes the characteristics of a physical surface.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class ElementOverviewThis class defines the material that makes up a PHASEShape object.You don’t instantiate instances of this class yourself; the framework creates an instance of this class for every material you pass into the init(engine:mesh:materials:) initializer. The shape’s elements array provides read-only access to the instances.TopicsSpecifying a Meterialvar material: PHASEMaterial?A surface characteristic that determines the acoustic properties of an object.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSoundscape Creationclass PHASESourceAn object that plays audio from a 3D location and orientation in a scene.class PHASEListenerA central point of reference that defines the location within the scene that’s most audible to the user.class PHASEOccluderAn object with a shape and position that blocks audio from reaching the listener.class PHASEObjectAn object in the scene.class PHASEShapeA collection of points that connect to form a 3D volume.class PHASEMaterialSurface characteristics that determine the acoustic properties of an object.enum PHASEMaterialPresetA collection of physical surfaces that each add a unique acoustic quality to your app’s audio.class PHASEMixerParametersAn object that specifies a mixer for sound events and orients them in 3D space.

#### material | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseshape/element/material

PHASE  PHASEShape  PHASEShape  PHASEShape.Element  material Instance PropertymaterialA surface characteristic that determines the acoustic properties of an object.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var material: PHASEMaterial? { get set }

### elements | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseshape/elements

PHASE  PHASEShape  elements Instance PropertyelementsAn array of objects that collectively describe the physical characteristics of a surface.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var elements: [PHASEShape.Element] { get }See AlsoDescribing Surface Characteristicsclass ElementAn object that describes the characteristics of a physical surface.

### init(engine:mesh:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseshape/init(engine:mesh:)

PHASE  PHASEShape  init(engine:mesh:) Initializerinit(engine:mesh:)Creates an object that the given geometric data shapes.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    engine: PHASEEngine,
    mesh: MDLMesh
) Parameters engineThe object that controls this class’s associated audio output.meshA collection of points that connect to form a shape.See AlsoCreating a Shapeconvenience init(engine: PHASEEngine, mesh: MDLMesh, materials: [PHASEMaterial])Creates an object of a specific material that the given geometric data shapes.

### init(engine:mesh:materials:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseshape/init(engine:mesh:materials:)

PHASE  PHASEShape  init(engine:mesh:materials:) Initializerinit(engine:mesh:materials:)Creates an object of a specific material that the given geometric data shapes.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+convenience init(
    engine: PHASEEngine,
    mesh: MDLMesh,
    materials: [PHASEMaterial]
) Parameters engineThe object that controls this class’s associated audio output.meshA collection of points that connect to form a shape.materialsAn array of objects that describe surface characteristics.DiscussionThe framework assigns a material from the material array for every submesh in the mesh object. For example, PHASE infers that the first mesh is wooden if the first element of the material array is PHASEMaterialPreset.wood.If the number of submeshes within the mesh is less than or equal to the material array count, each material indexes the corresponding element. If the number of submeshes is greater than the material array count, each material indexes the element at the element index modulo the material count.The framework generates an error for empty material arrays or nil array entries.See AlsoCreating a Shapeinit(engine: PHASEEngine, mesh: MDLMesh)Creates an object that the given geometric data shapes.

## PHASESoundAsset | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundasset

PHASE  PHASESoundAsset ClassPHASESoundAssetA sound resource stored in the asset registry.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASESoundAssetOverviewThis class wraps source audio data that an app intends to play. The framework requires a mixer to play a sound asset, and sound event nodes like PHASESamplerNodeDefinition combine the asset with a mixer. To provide a sound asset to a sound-event node, refer to the asset by the identifier you pass into the registerSoundAsset(url:identifier:assetType:channelLayout:normalizationMode:) function.TopicsAccessing Sound Datavar data: Data?A storage buffer for the sound asset.var url: URL?The URL of the sound asset.Classifying an Assetvar type: PHASEAsset.AssetTypeThe type of sound asset.RelationshipsInherits FromPHASEAssetConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoAudio Selection and Playbackclass PHASESoundEventAn object that determines which audio to play.enum RenderingStateThe playback status of audio.class PHASESoundEventNodeDefinitionA base class for sound event nodes that connect to form a node hierarchy.class PHASESoundEventNodeAssetA template object for sounds that can play in reaction to environmental state.class PHASEAssetA base class that adds a name to framework assets.API ReferenceSound Event NodesObjects that connect to form a hierarchical tree of audio actions.

### data | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundasset/data

PHASE  PHASESoundAsset  data Instance PropertydataA storage buffer for the sound asset.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var data: Data? { get }DiscussionThis property has a value when an app creates the asset with registerSoundAsset(data:identifier:format:normalizationMode:); otherwise the value is nil.See AlsoAccessing Sound Datavar url: URL?The URL of the sound asset.

### type | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundasset/type

PHASE  PHASESoundAsset  type Instance PropertytypeThe type of sound asset.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var type: PHASEAsset.AssetType { get }DiscussionThe framework sets the value of this property to the type you pass into registerSoundAsset(url:identifier:assetType:channelLayout:normalizationMode:).

### url | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundasset/url

PHASE  PHASESoundAsset  url Instance PropertyurlThe URL of the sound asset.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var url: URL? { get }DiscussionThis property has a value when an app creates the asset with registerSoundAsset(url:identifier:assetType:channelLayout:normalizationMode:); otherwise the value is nil.See AlsoAccessing Sound Datavar data: Data?A storage buffer for the sound asset.

## PHASESoundEvent | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent

PHASE  PHASESoundEvent ClassPHASESoundEventAn object that determines which audio to play.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASESoundEvent Mentioned in  Playing sound from a location in a 3D scene OverviewA sound event represents a logic tree, or hierarchy, that defines what, when, and how the framework plays a sound at runtime. You configure the tree with conditions based on your app’s state. When you invoke a sound event’s root node at runtime, the framework navigates the tree by branching based on the logic, landing on a playable node that sends the right audio to the output device:To invoke a specific one-time sound, create a sound event from a single sampler node.To invoke a sound event that tailors its sound based on your app’s state, define a sound event hierarchy containing one or more control nodes; see Sound Event Nodes. For example, to play either footsteps or a jumping noise depending on the hero’s state, you configure a switch node that navigates based on the hero’s hypothetical isJumping metaparameter.For sound event nodes that play audio, the asset’s playbackMode determines whether the audio loops. One-time sound events stop automatically at the end of the audio data. Looping sound events (those with playbackMode = PHASEPlaybackMode.looping) require you to explicitly call stopAndInvalidate() to stop the audio.Playing a one-shot channel-based soundApps create a sound event by requesting one from a sound event node asset. To create a sound event node asset, combine a sound asset (the source audio data) with a mixer object (which combines sound layers for output) to create a node, and add the node to the asset registry. By creating a sound event from a sampler node (PHASESamplerNodeDefinition), the following code plays an audio file once before discarding it.// Create a channel layout for audio types that contain no channel metadata. 
let stereoLayout = AVAudioChannelLayout(layoutTag: kAudioChannelLayoutTag_Stereo)    

// Load an audio file from the bundle.
let bangSoundURL = Bundle.main.url(forResource: "bangSound", withExtension: "wav")!

// Create and register a sound asset.
var bangSoundAsset:PHASESoundAsset!
do { 
    bangSoundAsset = try engine.assetRegistry.registerSoundAsset(
        url: bangSoundURL, 
        identifier: "bangSound", 
        assetType: .resident, 
        channelLayout: stereoLayout,
        normalizationMode: .dynamic)
} catch { print("Failed to register the sound asset.") }

// Create a mixer that routes sound directly to the output.
let stereoMixer = PHASEChannelMixerDefinition(channelLayout:stereoLayout!)

// Create a sound event node.
let bangSoundSamplerNode = PHASESamplerNodeDefinition(
    soundAssetIdentifier: bangSoundAsset.identifier, 
    mixerDefinition: stereoMixer, identifier:"bangSoundNode")

// Add the sound event node to the asset registry and retrieve the asset object.
var bangSoundSoundEventAsset: PHASESoundEventNodeAsset! 
do {
    bangSoundEventAsset = try engine.assetRegistry.registerSoundEventAsset(
        rootNode: bangSoundSamplerNode, identifier:"bangSoundTree")
} catch { print ("Failed to register the sound event node.") }
The resulting node asset represents a template for audio that’s ready for playback. To play the audio, spawn a sound event off of the node asset and call start(completion:) to invoke the sound event.// Create a playable sound event from the template sound event asset.
var bangSoundEvent: PHASESoundEvent!
do {
        bangSoundEvent = try PHASESoundEvent(engine:engine, 
        assetIdentifier: bangSoundEventAsset.identifier)
} catch { print ("Failed to create the sound event.") }

// Play the one-shot sound event.
bangSoundEvent.start()
Important To play the same sound asset again, create another sound event object. After the first start(completion:) call on a particular PHASESoundEvent instance, subsequent calls have no effect.TopicsCreating a Sound Eventinit(engine: PHASEEngine, assetIdentifier: String) throwsCreates a sound event node with the given asset.init(engine: PHASEEngine, assetIdentifier: String, mixerParameters: PHASEMixerParameters) throwsCreates a sound event node with the given asset and mixer parameters.Configuring Mixers and Metaparametersvar mixers: [String : PHASEMixer]Nodes in the event tree that control the volume of their child nodes.var metaParameters: [String : PHASEMetaParameter]The object’s meta parameters.Preparing Playbackfunc prepare(completion: ((PHASESoundEvent.PrepareHandlerReason) -> Void)?)Enables a sound event to play and runs the argument code when the sound event plays back.enum PrepareHandlerReasonIndicates the results of sound-event preparation.var prepareState: PHASESoundEvent.PrepareStateThe status of sound-event preparation.enum PrepareStateIndicates the state of sound-event preparation.Checking Playback Statusvar renderingState: PHASESoundEvent.RenderingStateThe sound event’s playback status.enum RenderingStateThe playback status of audio.Providing Buffered Datavar pushStreamNodes: [String : PHASEPushStreamNode]A collection of audio streams for playback.Starting Playbackfunc start(completion: ((PHASESoundEvent.StartHandlerReason) -> Void)?)Invokes the sound event and runs the specified code on completion.enum StartHandlerReasonIndicates the status after starting a sound event.Seeking a Timefunc seek(to: Double, completion: ((PHASESoundEvent.SeekHandlerReason) -> Void)?)Advances the sound event’s playback position to a specific time.enum SeekHandlerReasonIndicates the status after a sound event changes its playback position.Pausing Playbackfunc pause()Pauses the sound event.func resume()Resumes the sound event.Stopping Playbackfunc stopAndInvalidate()Stops a sound event and prevents it from resuming.var isIndefinite: BoolA Boolean value that indicates whether the sound loops or stops on its own.Instance Propertiesvar pullStreamNodes: [String : PHASEPullStreamNode]Instance Methodsfunc resume(at: AVAudioTime?)Betafunc seek(to: Double, resumeAt: AVAudioTime, completion: ((PHASESoundEvent.SeekHandlerReason) -> Void)?)Betafunc start(at: AVAudioTime?, completion: ((PHASESoundEvent.StartHandlerReason) -> Void)?)BetaRelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoAudio Selection and Playbackclass PHASESoundAssetA sound resource stored in the asset registry.enum RenderingStateThe playback status of audio.class PHASESoundEventNodeDefinitionA base class for sound event nodes that connect to form a node hierarchy.class PHASESoundEventNodeAssetA template object for sounds that can play in reaction to environmental state.class PHASEAssetA base class that adds a name to framework assets.API ReferenceSound Event NodesObjects that connect to form a hierarchical tree of audio actions.

### init(engine:assetIdentifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/init(engine:assetidentifier:)

PHASE  PHASESoundEvent  init(engine:assetIdentifier:) Initializerinit(engine:assetIdentifier:)Creates a sound event node with the given asset.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    engine: PHASEEngine,
    assetIdentifier: String
) throws Parameters engineThe object that controls this class’s associated audio output.assetIdentifierThe identifier for the sound event asset from which to create the node.See AlsoCreating a Sound Eventinit(engine: PHASEEngine, assetIdentifier: String, mixerParameters: PHASEMixerParameters) throwsCreates a sound event node with the given asset and mixer parameters.

### init(engine:assetIdentifier:mixerParameters:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/init(engine:assetidentifier:mixerparameters:)

PHASE  PHASESoundEvent  init(engine:assetIdentifier:mixerParameters:) Initializerinit(engine:assetIdentifier:mixerParameters:)Creates a sound event node with the given asset and mixer parameters.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    engine: PHASEEngine,
    assetIdentifier: String,
    mixerParameters: PHASEMixerParameters
) throws Parameters engineThe object that controls this class’s associated audio output.assetIdentifierThe identifier for the sound event asset from which to create the node.mixerParametersA dictionary of spatial mixer parameters to enable. The keys match available identifiers of the object’s spatial mixers.See AlsoCreating a Sound Eventinit(engine: PHASEEngine, assetIdentifier: String) throwsCreates a sound event node with the given asset.

### isIndefinite | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/isindefinite

PHASE  PHASESoundEvent  isIndefinite Instance PropertyisIndefiniteA Boolean value that indicates whether the sound loops or stops on its own.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var isIndefinite: Bool { get }See AlsoStopping Playbackfunc stopAndInvalidate()Stops a sound event and prevents it from resuming.

### metaParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/metaparameters

PHASE  PHASESoundEvent  metaParameters Instance PropertymetaParametersThe object’s meta parameters.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var metaParameters: [String : PHASEMetaParameter] { get }DiscussionEach meta parameter contained in this dictionary affects only the sound event instance when you change the parameter’s value at runtime. As a read-only dictionary, the framework sets the contents based on the parameter you pass into a node definition initializer, for example, init(switchMetaParameterDefinition:). The dictionary key is the identifier of the source PHASEMetaParameterDefinition.Tip To propagate a metaparameter change to multiple sound events instead of just one, register the metaparameter globally by calling registerGlobalMetaParameter(metaParameterDefinition:). To change its value, access the metaparameter through the asset registry’s globalMetaParameters dictionary instead.See AlsoConfiguring Mixers and Metaparametersvar mixers: [String : PHASEMixer]Nodes in the event tree that control the volume of their child nodes.

### mixers | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/mixers

PHASE  PHASESoundEvent  mixers Instance PropertymixersNodes in the event tree that control the volume of their child nodes.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var mixers: [String : PHASEMixer] { get }See AlsoConfiguring Mixers and Metaparametersvar metaParameters: [String : PHASEMetaParameter]The object’s meta parameters.

### pause() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/pause()

PHASE  PHASESoundEvent  pause() Instance Methodpause()Pauses the sound event.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func pause()DiscussionIf the sound event plays audio, this function pauses audio playback.See AlsoPausing Playbackfunc resume()Resumes the sound event.

### prepare(completion:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/prepare(completion:)

PHASE  PHASESoundEvent  prepare(completion:) Instance Methodprepare(completion:)Enables a sound event to play and runs the argument code when the sound event plays back.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func prepare(completion handler: ((PHASESoundEvent.PrepareHandlerReason) -> Void)? = nil)func prepare() async -> PHASESoundEvent.PrepareHandlerReason Parameters handlerCode the framework runs when sound event preparation completes. If you pass nil, no code runs when preparation completes.DiscussionImportant You can call this method from synchronous code using a completion handler, as shown on this page, or you can call it as an asynchronous method that has the following declaration:func prepare() async -> PHASESoundEvent.PrepareHandlerReason
For information about concurrency and asynchronous code in Swift, see Calling Objective-C APIs Asynchronously.This function instructs the engine to prepare a sound event and returns immediately. When the preparation completes or fails, the framework runs completionHandler.If you call start(completion:) before completionHandler runs, the framework queues the sound event to occur when preparation completes.See AlsoPreparing Playbackenum PrepareHandlerReasonIndicates the results of sound-event preparation.var prepareState: PHASESoundEvent.PrepareStateThe status of sound-event preparation.enum PrepareStateIndicates the state of sound-event preparation.

### PHASESoundEvent.PrepareHandlerReason | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/preparehandlerreason

PHASE  PHASESoundEvent  PHASESoundEvent.PrepareHandlerReason EnumerationPHASESoundEvent.PrepareHandlerReasonIndicates the results of sound-event preparation.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum PrepareHandlerReasonOverviewThe sound event prepare(completion:) function passes an instance of this class to its argument completion closure to communicate the results of the call.TopicsReasonscase preparedIndicates the completion of sound-event preparation.case terminatedIndicates sound-event preparation stops abruptly.case failureIndicates an error occurs during sound-event preparation.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoPreparing Playbackfunc prepare(completion: ((PHASESoundEvent.PrepareHandlerReason) -> Void)?)Enables a sound event to play and runs the argument code when the sound event plays back.var prepareState: PHASESoundEvent.PrepareStateThe status of sound-event preparation.enum PrepareStateIndicates the state of sound-event preparation.

#### PHASESoundEvent.PrepareHandlerReason.failure | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/preparehandlerreason/failure

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.PrepareHandlerReason  PHASESoundEvent.PrepareHandlerReason.failure CasePHASESoundEvent.PrepareHandlerReason.failureIndicates an error occurs during sound-event preparation.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case failureSee AlsoReasonscase preparedIndicates the completion of sound-event preparation.case terminatedIndicates sound-event preparation stops abruptly.

#### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/preparehandlerreason/init(rawvalue:)

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.PrepareHandlerReason  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

#### PHASESoundEvent.PrepareHandlerReason.prepared | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/preparehandlerreason/prepared

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.PrepareHandlerReason  PHASESoundEvent.PrepareHandlerReason.prepared CasePHASESoundEvent.PrepareHandlerReason.preparedIndicates the completion of sound-event preparation.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case preparedSee AlsoReasonscase terminatedIndicates sound-event preparation stops abruptly.case failureIndicates an error occurs during sound-event preparation.

#### PHASESoundEvent.PrepareHandlerReason.terminated | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/preparehandlerreason/terminated

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.PrepareHandlerReason  PHASESoundEvent.PrepareHandlerReason.terminated CasePHASESoundEvent.PrepareHandlerReason.terminatedIndicates sound-event preparation stops abruptly.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case terminatedSee AlsoReasonscase preparedIndicates the completion of sound-event preparation.case failureIndicates an error occurs during sound-event preparation.

### PHASESoundEvent.PrepareState | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/preparestate-swift.enum

PHASE  PHASESoundEvent  PHASESoundEvent.PrepareState EnumerationPHASESoundEvent.PrepareStateIndicates the state of sound-event preparation.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum PrepareStateTopicsStatescase prepareInProgressIndicates that the sound event prepares for playback.case prepareNotStartedIndicates that the sound event awaits preparation.case preparedIndicates that the sound event preparation is complete.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoPreparing Playbackfunc prepare(completion: ((PHASESoundEvent.PrepareHandlerReason) -> Void)?)Enables a sound event to play and runs the argument code when the sound event plays back.enum PrepareHandlerReasonIndicates the results of sound-event preparation.var prepareState: PHASESoundEvent.PrepareStateThe status of sound-event preparation.

#### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/preparestate-swift.enum/init(rawvalue:)

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.PrepareState  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

#### PHASESoundEvent.PrepareState.prepared | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/preparestate-swift.enum/prepared

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.PrepareState  PHASESoundEvent.PrepareState.prepared CasePHASESoundEvent.PrepareState.preparedIndicates that the sound event preparation is complete.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case preparedSee AlsoStatescase prepareInProgressIndicates that the sound event prepares for playback.case prepareNotStartedIndicates that the sound event awaits preparation.

#### PHASESoundEvent.PrepareState.prepareInProgress | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/preparestate-swift.enum/prepareinprogress

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.PrepareState  PHASESoundEvent.PrepareState.prepareInProgress CasePHASESoundEvent.PrepareState.prepareInProgressIndicates that the sound event prepares for playback.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case prepareInProgressSee AlsoStatescase prepareNotStartedIndicates that the sound event awaits preparation.case preparedIndicates that the sound event preparation is complete.

#### PHASESoundEvent.PrepareState.prepareNotStarted | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/preparestate-swift.enum/preparenotstarted

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.PrepareState  PHASESoundEvent.PrepareState.prepareNotStarted CasePHASESoundEvent.PrepareState.prepareNotStartedIndicates that the sound event awaits preparation.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case prepareNotStartedSee AlsoStatescase prepareInProgressIndicates that the sound event prepares for playback.case preparedIndicates that the sound event preparation is complete.

### prepareState | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/preparestate-swift.property

PHASE  PHASESoundEvent  prepareState Instance PropertyprepareStateThe status of sound-event preparation.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var prepareState: PHASESoundEvent.PrepareState { get }See AlsoPreparing Playbackfunc prepare(completion: ((PHASESoundEvent.PrepareHandlerReason) -> Void)?)Enables a sound event to play and runs the argument code when the sound event plays back.enum PrepareHandlerReasonIndicates the results of sound-event preparation.enum PrepareStateIndicates the state of sound-event preparation.

### pullStreamNodes | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/pullstreamnodes

PHASE  PHASESoundEvent  pullStreamNodes Instance PropertypullStreamNodesiOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 2.0+var pullStreamNodes: [String : PHASEPullStreamNode] { get }DiscussionA Dictionary containing the pull stream nodes associated with this sound event, for setting renderBlocks on.

### pushStreamNodes | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/pushstreamnodes

PHASE  PHASESoundEvent  pushStreamNodes Instance PropertypushStreamNodesA collection of audio streams for playback.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var pushStreamNodes: [String : PHASEPushStreamNode] { get }DiscussionThis dictionary populates a push-stream node for sound events that PHASE generates for PHASEPushStreamNodeDefinition in your event node tree. The dictionary key is the stream-node definition’s identifier.

### PHASESoundEvent.RenderingState | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/renderingstate-swift.enum

PHASE  PHASESoundEvent  PHASESoundEvent.RenderingState EnumerationPHASESoundEvent.RenderingStateThe playback status of audio.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum RenderingStateOverviewThis enumeration defines the possible values of:A sound event’s renderingState propertyThe engine’s renderingState propertyTopicsStatescase pausedA state in which sound event playback pauses.case startedA state in which sound event playback starts.case stoppedA state in which sound event playback stops.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoAudio Selection and Playbackclass PHASESoundAssetA sound resource stored in the asset registry.class PHASESoundEventAn object that determines which audio to play.class PHASESoundEventNodeDefinitionA base class for sound event nodes that connect to form a node hierarchy.class PHASESoundEventNodeAssetA template object for sounds that can play in reaction to environmental state.class PHASEAssetA base class that adds a name to framework assets.API ReferenceSound Event NodesObjects that connect to form a hierarchical tree of audio actions.

#### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/renderingstate-swift.enum/init(rawvalue:)

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.RenderingState  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

#### PHASESoundEvent.RenderingState.paused | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/renderingstate-swift.enum/paused

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.RenderingState  PHASESoundEvent.RenderingState.paused CasePHASESoundEvent.RenderingState.pausedA state in which sound event playback pauses.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case pausedSee AlsoStatescase startedA state in which sound event playback starts.case stoppedA state in which sound event playback stops.

#### PHASESoundEvent.RenderingState.started | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/renderingstate-swift.enum/started

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.RenderingState  PHASESoundEvent.RenderingState.started CasePHASESoundEvent.RenderingState.startedA state in which sound event playback starts.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case startedSee AlsoStatescase pausedA state in which sound event playback pauses.case stoppedA state in which sound event playback stops.

#### PHASESoundEvent.RenderingState.stopped | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/renderingstate-swift.enum/stopped

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.RenderingState  PHASESoundEvent.RenderingState.stopped CasePHASESoundEvent.RenderingState.stoppedA state in which sound event playback stops.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case stoppedSee AlsoStatescase pausedA state in which sound event playback pauses.case startedA state in which sound event playback starts.

### renderingState | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/renderingstate-swift.property

PHASE  PHASESoundEvent  renderingState Instance PropertyrenderingStateThe sound event’s playback status.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var renderingState: PHASESoundEvent.RenderingState { get }DiscussionAccess this property to check the sound event’s playback status. The value reflects the state you control by calling one of the functions: start(completion:), stopAndInvalidate(), or pause().See AlsoChecking Playback Statusenum RenderingStateThe playback status of audio.

### Web Server Error
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/resume()

Web Server Error

Description: The host did not return the document correctly.

### resume(at:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/resume(at:)

PHASE  PHASESoundEvent  PHASESoundEvent  resume(at:) BetaInstance Methodresume(at:)iOS 26.0+BetaiPadOS 26.0+BetaMac Catalyst 26.0+BetamacOS 26.0+BetatvOS 26.0+BetavisionOS 26.0+Betafunc resume(at time: AVAudioTime?) Parameters timeThe desired start time based on the engine time retrieved from [PHASEEngine lastRenderTime]DiscussionResume the sound event at a specific timeA nil time parameter will resume immediately. The device time is not scaled by UnitsPerSecond and is in seconds.Beta Software This documentation contains preliminary information about an API or technology in development. This information is subject to change, and software implemented according to this documentation should be tested with final operating system software.  Learn more about using Apple's beta software

### seek(to:completion:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/seek(to:completion:)

PHASE  PHASESoundEvent  seek(to:completion:) Instance Methodseek(to:completion:)Advances the sound event’s playback position to a specific time.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func seek(
    to time: Double,
    completion handler: ((PHASESoundEvent.SeekHandlerReason) -> Void)? = nil
)func seek(to time: Double) async -> PHASESoundEvent.SeekHandlerReason Parameters timeThe playback position to advance to. The framework scales this value by unitsPerSecond.DiscussionImportant You can call this method from synchronous code using a completion handler, as shown on this page, or you can call it as an asynchronous method that has the following declaration:func seek(to time: Double) async -> PHASESoundEvent.SeekHandlerReason
For information about concurrency and asynchronous code in Swift, see Calling Objective-C APIs Asynchronously.See AlsoSeeking a Timeenum SeekHandlerReasonIndicates the status after a sound event changes its playback position.

### seek(to:resumeAt:completion:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/seek(to:resumeat:completion:)

PHASE  PHASESoundEvent  PHASESoundEvent  seek(to:resumeAt:completion:) BetaInstance Methodseek(to:resumeAt:completion:)iOS 26.0+BetaiPadOS 26.0+BetaMac Catalyst 26.0+BetamacOS 26.0+BetatvOS 26.0+BetavisionOS 26.0+Betafunc seek(
    to time: Double,
    resumeAt engineTime: AVAudioTime,
    completion handler: ((PHASESoundEvent.SeekHandlerReason) -> Void)? = nil
)func seek(
    to time: Double,
    resumeAt engineTime: AVAudioTime
) async -> PHASESoundEvent.SeekHandlerReason Parameters timeThe desired time position in seconds to seek the nodes to.engineTimeThe engine time to resume playback.handlerThe completion callback that will be called when seeking is complete.DiscussionSeeks all leaf nodes in a PHASESoundEvent to the specified time, and automatically resumes playback at the specified engine time.This is a low latency convenience method that allows for tight deadlines to be met.  However if the seek fails the node state will not be changed.  You should check the callback and handle the failure appropriately. The time parameter will seek the nodes to the equivalent sample position based on the sample rate of the asset. The engineTime parameter is the engine timestamp to resume rendering at, based off of [PHASEEngine lastRenderTime]. If any leaf nodes do not support seeking, those nodes will ignore this command. Nodes that have finished playing or have stopped will not seek. The time parameter is in seconds and will be scaled by unitsPerSecond. The time in the AVAudioTime structure is not scaled by unitsPerSecond. The engineTime parameter will use the sample time if valid, if not, then the host time if valid.Beta Software This documentation contains preliminary information about an API or technology in development. This information is subject to change, and software implemented according to this documentation should be tested with final operating system software.  Learn more about using Apple's beta software

### PHASESoundEvent.SeekHandlerReason | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/seekhandlerreason

PHASE  PHASESoundEvent  PHASESoundEvent.SeekHandlerReason EnumerationPHASESoundEvent.SeekHandlerReasonIndicates the status after a sound event changes its playback position.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum SeekHandlerReasonOverviewWhen your app changes the playback position of a sound event by calling seek(to:completion:), the framework invokes the argument closure when the seek succeeds or fails. PHASE passes an instance of this enumeration to the closure to describe the results of the call.TopicsReasonscase seekSuccessfulIndicates the sound event successfully updated its playback position.case failureSeekAlreadyInProgressIndicates the sound event is still updating its playback position.case failureIndicates the sound event fails to update its playback position.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoSeeking a Timefunc seek(to: Double, completion: ((PHASESoundEvent.SeekHandlerReason) -> Void)?)Advances the sound event’s playback position to a specific time.

#### PHASESoundEvent.SeekHandlerReason.failure | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/seekhandlerreason/failure

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.SeekHandlerReason  PHASESoundEvent.SeekHandlerReason.failure CasePHASESoundEvent.SeekHandlerReason.failureIndicates the sound event fails to update its playback position.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case failureSee AlsoReasonscase seekSuccessfulIndicates the sound event successfully updated its playback position.case failureSeekAlreadyInProgressIndicates the sound event is still updating its playback position.

#### PHASESoundEvent.SeekHandlerReason.failureSeekAlreadyInProgress | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/seekhandlerreason/failureseekalreadyinprogress

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.SeekHandlerReason  PHASESoundEvent.SeekHandlerReason.failureSeekAlreadyInProgress CasePHASESoundEvent.SeekHandlerReason.failureSeekAlreadyInProgressIndicates the sound event is still updating its playback position.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case failureSeekAlreadyInProgressSee AlsoReasonscase seekSuccessfulIndicates the sound event successfully updated its playback position.case failureIndicates the sound event fails to update its playback position.

#### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/seekhandlerreason/init(rawvalue:)

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.SeekHandlerReason  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

#### PHASESoundEvent.SeekHandlerReason.seekSuccessful | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/seekhandlerreason/seeksuccessful

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.SeekHandlerReason  PHASESoundEvent.SeekHandlerReason.seekSuccessful CasePHASESoundEvent.SeekHandlerReason.seekSuccessfulIndicates the sound event successfully updated its playback position.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case seekSuccessfulSee AlsoReasonscase failureSeekAlreadyInProgressIndicates the sound event is still updating its playback position.case failureIndicates the sound event fails to update its playback position.

### start(at:completion:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/start(at:completion:)

PHASE  PHASESoundEvent  PHASESoundEvent  start(at:completion:) BetaInstance Methodstart(at:completion:)iOS 26.0+BetaiPadOS 26.0+BetaMac Catalyst 26.0+BetamacOS 26.0+BetatvOS 26.0+BetavisionOS 26.0+Betafunc start(
    at when: AVAudioTime?,
    completion handler: ((PHASESoundEvent.StartHandlerReason) -> Void)? = nil
)func start(at when: AVAudioTime?) async -> PHASESoundEvent.StartHandlerReason Parameters whenThe desired start time based on the engine time retrieved from [PHASEEngine lastRenderTime] If the sound event starts immediately with an audible sound, it will begin rendering at this time.  The sound event will otherwise begin operating at this time. A nil value will start the sound event immediately This time is not scaled by unitsPerSecond.handlerThe block that will be called when the sound event has stopped.DiscussionStart the sound eventThis function notifies the engine to start the sound event, then returns immediately. Once the sound event is playing (or has failed to start), you will receive a callback via the completion. Playback will begin at the requested time if the sound event has finished preparing in time. You may wait for preparation to finish with the [PHASESoundEvent prepare:completion] method before calling startAtTime, to ensure that the sound event will start at the desired time. However if the desired time is far enough into the future to allow for preparation to happen, you may skip calling prepare entirely and just call startAtTime.Beta Software This documentation contains preliminary information about an API or technology in development. This information is subject to change, and software implemented according to this documentation should be tested with final operating system software.  Learn more about using Apple's beta software

### start(completion:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/start(completion:)

PHASE  PHASESoundEvent  start(completion:) Instance Methodstart(completion:)Invokes the sound event and runs the specified code on completion.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func start(completion handler: ((PHASESoundEvent.StartHandlerReason) -> Void)? = nil)func start() async -> PHASESoundEvent.StartHandlerReason Mentioned in  Playing sound from a location in a 3D scene DiscussionImportant You can call this method from synchronous code using a completion handler, as shown on this page, or you can call it as an asynchronous method that has the following declaration:func start() async -> PHASESoundEvent.StartHandlerReason
For information about concurrency and asynchronous code in Swift, see Calling Objective-C APIs Asynchronously.This function returns immediately after instructing the engine to invoke the sound event. If a problem occurs, the function provides an error.The sound event’s audio plays immediately if the app prepares the sound event in advance. Otherwise, the sound event begins preparing and then plays after preparation completes.When the sound event plays or errors out, the framework invokes completionHandler, passing in a PHASESoundEvent.StartHandlerReason that explains the reason for the invocation.Important To play the same sound asset again, create another sound event object. After the first start(completion:) call on a particular PHASESoundEvent instance, subsequent calls have no effect.See AlsoStarting Playbackenum StartHandlerReasonIndicates the status after starting a sound event.

### PHASESoundEvent.StartHandlerReason | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/starthandlerreason

PHASE  PHASESoundEvent  PHASESoundEvent.StartHandlerReason EnumerationPHASESoundEvent.StartHandlerReasonIndicates the status after starting a sound event.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum StartHandlerReasonOverviewWhen your app starts a sound event by calling start(completion:), the framework invokes the argument closure when starting succeeds or fails. PHASE passes an instance of this enumeration to the closure to describe the results of the call.TopicsReasonscase finishedPlayingIndicates the framework successfully started the sound event.case terminatedIndicates the framework terminated the sound event abruptly.case failureIndicates an error occurred while starting the sound event.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoStarting Playbackfunc start(completion: ((PHASESoundEvent.StartHandlerReason) -> Void)?)Invokes the sound event and runs the specified code on completion.

#### PHASESoundEvent.StartHandlerReason.failure | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/starthandlerreason/failure

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.StartHandlerReason  PHASESoundEvent.StartHandlerReason.failure CasePHASESoundEvent.StartHandlerReason.failureIndicates an error occurred while starting the sound event.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case failureSee AlsoReasonscase finishedPlayingIndicates the framework successfully started the sound event.case terminatedIndicates the framework terminated the sound event abruptly.

#### PHASESoundEvent.StartHandlerReason.finishedPlaying | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/starthandlerreason/finishedplaying

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.StartHandlerReason  PHASESoundEvent.StartHandlerReason.finishedPlaying CasePHASESoundEvent.StartHandlerReason.finishedPlayingIndicates the framework successfully started the sound event.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case finishedPlayingSee AlsoReasonscase terminatedIndicates the framework terminated the sound event abruptly.case failureIndicates an error occurred while starting the sound event.

#### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/starthandlerreason/init(rawvalue:)

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.StartHandlerReason  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

#### PHASESoundEvent.StartHandlerReason.terminated | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/starthandlerreason/terminated

PHASE  PHASESoundEvent  PHASESoundEvent  PHASESoundEvent.StartHandlerReason  PHASESoundEvent.StartHandlerReason.terminated CasePHASESoundEvent.StartHandlerReason.terminatedIndicates the framework terminated the sound event abruptly.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case terminatedSee AlsoReasonscase finishedPlayingIndicates the framework successfully started the sound event.case failureIndicates an error occurred while starting the sound event.

### stopAndInvalidate() | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundevent/stopandinvalidate()

PHASE  PHASESoundEvent  stopAndInvalidate() Instance MethodstopAndInvalidate()Stops a sound event and prevents it from resuming.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func stopAndInvalidate()See AlsoStopping Playbackvar isIndefinite: BoolA Boolean value that indicates whether the sound loops or stops on its own.

## PHASESoundEventError | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerror-swift.struct

PHASE  PHASESoundEventError StructurePHASESoundEventErrorA sound event error that PHASE reports.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+struct PHASESoundEventErrorTopicsCreating an Errorenum CodeCodes that identify sound event errors.Identifying an Error Causestatic var apiMisuse: PHASESoundEventError.CodeAn error that indicates the app misconfigures data or calls the framework in unsupported succession.static var badData: PHASESoundEventError.CodeAn error that indicates a sound event contains invalid data.static var invalidInstance: PHASESoundEventError.CodeAn error that indicates a sound event object is no longer valid.static var notFound: PHASESoundEventError.CodeAn error the framework throws when it fails to find a particular sound event.static var outOfMemory: PHASESoundEventError.CodeAn error the framework throws when a sound event depletes system memory.static var systemNotInitialized: PHASESoundEventError.CodeAn error the framework throws when engine initialization interrupts sound event playback.Type Propertiesstatic var errorDomain: StringRelationshipsConforms ToCustomNSErrorEquatableErrorHashableSendableSendableMetatypeSee AlsoSound Event Errorsenum CodeCodes that identify sound event errors.let PHASESoundEventErrorDomain: StringA unique error domain for sound events.

### apiMisuse | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerror-swift.struct/apimisuse

PHASE  PHASESoundEventError  apiMisuse Type PropertyapiMisuseAn error that indicates the app misconfigures data or calls the framework in unsupported succession.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var apiMisuse: PHASESoundEventError.Code { get }See AlsoIdentifying an Error Causestatic var badData: PHASESoundEventError.CodeAn error that indicates a sound event contains invalid data.static var invalidInstance: PHASESoundEventError.CodeAn error that indicates a sound event object is no longer valid.static var notFound: PHASESoundEventError.CodeAn error the framework throws when it fails to find a particular sound event.static var outOfMemory: PHASESoundEventError.CodeAn error the framework throws when a sound event depletes system memory.static var systemNotInitialized: PHASESoundEventError.CodeAn error the framework throws when engine initialization interrupts sound event playback.

### badData | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerror-swift.struct/baddata

PHASE  PHASESoundEventError  badData Type PropertybadDataAn error that indicates a sound event contains invalid data.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var badData: PHASESoundEventError.Code { get }See AlsoIdentifying an Error Causestatic var apiMisuse: PHASESoundEventError.CodeAn error that indicates the app misconfigures data or calls the framework in unsupported succession.static var invalidInstance: PHASESoundEventError.CodeAn error that indicates a sound event object is no longer valid.static var notFound: PHASESoundEventError.CodeAn error the framework throws when it fails to find a particular sound event.static var outOfMemory: PHASESoundEventError.CodeAn error the framework throws when a sound event depletes system memory.static var systemNotInitialized: PHASESoundEventError.CodeAn error the framework throws when engine initialization interrupts sound event playback.

### PHASESoundEventError.Code | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerror-swift.struct/code

PHASE  PHASESoundEventError  PHASESoundEventError.Code EnumerationPHASESoundEventError.CodeCodes that identify sound event errors.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum CodeTopicsErrorscase apiMisuseAn error that indicates the app misconfigures data or calls the framework in unsupported succession.case badDataAn error that indicates a sound event contains invalid data.case invalidInstanceAn error that indicates a sound event object is no longer valid.case notFoundAn error the framework throws when it fails to find a particular sound event.case outOfMemoryAn error the framework throws when a sound event depletes system memory.case systemNotInitializedAn error the framework throws when engine initialization interrupts sound event playback.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoSound Event Errorsstruct PHASESoundEventErrorA sound event error that PHASE reports.let PHASESoundEventErrorDomain: StringA unique error domain for sound events.

#### PHASESoundEventError.Code.apiMisuse | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerror-swift.struct/code/apimisuse

PHASE  PHASESoundEventError  PHASESoundEventError  PHASESoundEventError.Code  PHASESoundEventError.Code.apiMisuse CasePHASESoundEventError.Code.apiMisuseAn error that indicates the app misconfigures data or calls the framework in unsupported succession.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case apiMisuseSee AlsoErrorscase badDataAn error that indicates a sound event contains invalid data.case invalidInstanceAn error that indicates a sound event object is no longer valid.case notFoundAn error the framework throws when it fails to find a particular sound event.case outOfMemoryAn error the framework throws when a sound event depletes system memory.case systemNotInitializedAn error the framework throws when engine initialization interrupts sound event playback.

#### PHASESoundEventError.Code.badData | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerror-swift.struct/code/baddata

PHASE  PHASESoundEventError  PHASESoundEventError  PHASESoundEventError.Code  PHASESoundEventError.Code.badData CasePHASESoundEventError.Code.badDataAn error that indicates a sound event contains invalid data.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case badDataSee AlsoErrorscase apiMisuseAn error that indicates the app misconfigures data or calls the framework in unsupported succession.case invalidInstanceAn error that indicates a sound event object is no longer valid.case notFoundAn error the framework throws when it fails to find a particular sound event.case outOfMemoryAn error the framework throws when a sound event depletes system memory.case systemNotInitializedAn error the framework throws when engine initialization interrupts sound event playback.

#### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerror-swift.struct/code/init(rawvalue:)

PHASE  PHASESoundEventError  PHASESoundEventError  PHASESoundEventError.Code  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

#### PHASESoundEventError.Code.invalidInstance | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerror-swift.struct/code/invalidinstance

PHASE  PHASESoundEventError  PHASESoundEventError  PHASESoundEventError.Code  PHASESoundEventError.Code.invalidInstance CasePHASESoundEventError.Code.invalidInstanceAn error that indicates a sound event object is no longer valid.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case invalidInstanceSee AlsoErrorscase apiMisuseAn error that indicates the app misconfigures data or calls the framework in unsupported succession.case badDataAn error that indicates a sound event contains invalid data.case notFoundAn error the framework throws when it fails to find a particular sound event.case outOfMemoryAn error the framework throws when a sound event depletes system memory.case systemNotInitializedAn error the framework throws when engine initialization interrupts sound event playback.

#### PHASESoundEventError.Code.notFound | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerror-swift.struct/code/notfound

PHASE  PHASESoundEventError  PHASESoundEventError  PHASESoundEventError.Code  PHASESoundEventError.Code.notFound CasePHASESoundEventError.Code.notFoundAn error the framework throws when it fails to find a particular sound event.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case notFoundSee AlsoErrorscase apiMisuseAn error that indicates the app misconfigures data or calls the framework in unsupported succession.case badDataAn error that indicates a sound event contains invalid data.case invalidInstanceAn error that indicates a sound event object is no longer valid.case outOfMemoryAn error the framework throws when a sound event depletes system memory.case systemNotInitializedAn error the framework throws when engine initialization interrupts sound event playback.

#### PHASESoundEventError.Code.outOfMemory | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerror-swift.struct/code/outofmemory

PHASE  PHASESoundEventError  PHASESoundEventError  PHASESoundEventError.Code  PHASESoundEventError.Code.outOfMemory CasePHASESoundEventError.Code.outOfMemoryAn error the framework throws when a sound event depletes system memory.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case outOfMemorySee AlsoErrorscase apiMisuseAn error that indicates the app misconfigures data or calls the framework in unsupported succession.case badDataAn error that indicates a sound event contains invalid data.case invalidInstanceAn error that indicates a sound event object is no longer valid.case notFoundAn error the framework throws when it fails to find a particular sound event.case systemNotInitializedAn error the framework throws when engine initialization interrupts sound event playback.

#### PHASESoundEventError.Code.systemNotInitialized | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerror-swift.struct/code/systemnotinitialized

PHASE  PHASESoundEventError  PHASESoundEventError  PHASESoundEventError.Code  PHASESoundEventError.Code.systemNotInitialized CasePHASESoundEventError.Code.systemNotInitializedAn error the framework throws when engine initialization interrupts sound event playback.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case systemNotInitializedSee AlsoErrorscase apiMisuseAn error that indicates the app misconfigures data or calls the framework in unsupported succession.case badDataAn error that indicates a sound event contains invalid data.case invalidInstanceAn error that indicates a sound event object is no longer valid.case notFoundAn error the framework throws when it fails to find a particular sound event.case outOfMemoryAn error the framework throws when a sound event depletes system memory.

### errorDomain | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerror-swift.struct/errordomain

PHASE  PHASESoundEventError  errorDomain Type PropertyerrorDomainiOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var errorDomain: String { get }

### invalidInstance | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerror-swift.struct/invalidinstance

PHASE  PHASESoundEventError  invalidInstance Type PropertyinvalidInstanceAn error that indicates a sound event object is no longer valid.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var invalidInstance: PHASESoundEventError.Code { get }See AlsoIdentifying an Error Causestatic var apiMisuse: PHASESoundEventError.CodeAn error that indicates the app misconfigures data or calls the framework in unsupported succession.static var badData: PHASESoundEventError.CodeAn error that indicates a sound event contains invalid data.static var notFound: PHASESoundEventError.CodeAn error the framework throws when it fails to find a particular sound event.static var outOfMemory: PHASESoundEventError.CodeAn error the framework throws when a sound event depletes system memory.static var systemNotInitialized: PHASESoundEventError.CodeAn error the framework throws when engine initialization interrupts sound event playback.

### notFound | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerror-swift.struct/notfound

PHASE  PHASESoundEventError  notFound Type PropertynotFoundAn error the framework throws when it fails to find a particular sound event.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var notFound: PHASESoundEventError.Code { get }See AlsoIdentifying an Error Causestatic var apiMisuse: PHASESoundEventError.CodeAn error that indicates the app misconfigures data or calls the framework in unsupported succession.static var badData: PHASESoundEventError.CodeAn error that indicates a sound event contains invalid data.static var invalidInstance: PHASESoundEventError.CodeAn error that indicates a sound event object is no longer valid.static var outOfMemory: PHASESoundEventError.CodeAn error the framework throws when a sound event depletes system memory.static var systemNotInitialized: PHASESoundEventError.CodeAn error the framework throws when engine initialization interrupts sound event playback.

### outOfMemory | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerror-swift.struct/outofmemory

PHASE  PHASESoundEventError  outOfMemory Type PropertyoutOfMemoryAn error the framework throws when a sound event depletes system memory.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var outOfMemory: PHASESoundEventError.Code { get }See AlsoIdentifying an Error Causestatic var apiMisuse: PHASESoundEventError.CodeAn error that indicates the app misconfigures data or calls the framework in unsupported succession.static var badData: PHASESoundEventError.CodeAn error that indicates a sound event contains invalid data.static var invalidInstance: PHASESoundEventError.CodeAn error that indicates a sound event object is no longer valid.static var notFound: PHASESoundEventError.CodeAn error the framework throws when it fails to find a particular sound event.static var systemNotInitialized: PHASESoundEventError.CodeAn error the framework throws when engine initialization interrupts sound event playback.

### systemNotInitialized | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerror-swift.struct/systemnotinitialized

PHASE  PHASESoundEventError  systemNotInitialized Type PropertysystemNotInitializedAn error the framework throws when engine initialization interrupts sound event playback.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var systemNotInitialized: PHASESoundEventError.Code { get }See AlsoIdentifying an Error Causestatic var apiMisuse: PHASESoundEventError.CodeAn error that indicates the app misconfigures data or calls the framework in unsupported succession.static var badData: PHASESoundEventError.CodeAn error that indicates a sound event contains invalid data.static var invalidInstance: PHASESoundEventError.CodeAn error that indicates a sound event object is no longer valid.static var notFound: PHASESoundEventError.CodeAn error the framework throws when it fails to find a particular sound event.static var outOfMemory: PHASESoundEventError.CodeAn error the framework throws when a sound event depletes system memory.

## PHASESoundEventErrorDomain | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventerrordomain

PHASE  PHASESoundEventErrorDomain Global VariablePHASESoundEventErrorDomainA unique error domain for sound events.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+let PHASESoundEventErrorDomain: StringDiscussionFor more information on Core Foundation error domains, see Error domains.See AlsoSound Event Errorsstruct PHASESoundEventErrorA sound event error that PHASE reports.enum CodeCodes that identify sound event errors.

## PHASESoundEventNodeAsset | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventnodeasset

PHASE  PHASESoundEventNodeAsset ClassPHASESoundEventNodeAssetA template object for sounds that can play in reaction to environmental state.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASESoundEventNodeAssetOverviewThis object refers by name to a collection of sound event nodes that connect to form a tree, or hierarchy. To retrieve an instance of this class, add a sound-event node definition to the asset registry using registerSoundEventAsset(rootNode:identifier:). Choose the rootNode argument from the subclasses in Sound Event Nodes based on the playback features your app requires.To play a single audio asset, register a rootNode with only one audio-providing node. Alternatively, to create a sound event that can change its audio based on your app’s current state, register a rootNode that contains children. By adding multiple nodes that play varying audio as children to a control node, PHASE plays the right audio for the moment based on control logic that you define.To create a playable sound event from this class, pass identifier to the assetIdentifier parameter of the sound event intializer, init(engine:assetIdentifier:). Then, invoke the sound event by calling start(completion:).As an opaque derived object, this class adds no properties to its base class.RelationshipsInherits FromPHASEAssetConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoAudio Selection and Playbackclass PHASESoundAssetA sound resource stored in the asset registry.class PHASESoundEventAn object that determines which audio to play.enum RenderingStateThe playback status of audio.class PHASESoundEventNodeDefinitionA base class for sound event nodes that connect to form a node hierarchy.class PHASEAssetA base class that adds a name to framework assets.API ReferenceSound Event NodesObjects that connect to form a hierarchical tree of audio actions.

## PHASESoundEventNodeDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventnodedefinition

PHASE  PHASESoundEventNodeDefinition ClassPHASESoundEventNodeDefinitionA base class for sound event nodes that connect to form a node hierarchy.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASESoundEventNodeDefinitionOverviewThis class defines the base functionality for an object that, depending on the derived class’s type, either plays audio or hands off the invocation to one or more other nodes.Configure a Sound Event Node to Play AudioTo play audio with this class, retrieve a sound-event node asset (PHASESoundEventNodeAsset) that generates sound events by creating and registering one of the audio-providing node definitions in Sound Event Nodes. Call registerSoundEventAsset(rootNode:identifier:) and pass the node definition in the rootNode argument. Provide an identifier argument with a unique name that your app refers to later when generating a playable PHASESoundEvent.Configure a Node Hiearchy that Reacts to Your App’s StateYou can create a hierarchy of nodes that blends audio based on your app’s parameters, or plays the right audio based on your app’s state. To create the hierarchy, register one of the control nodes in Sound Event Nodes by calling registerSoundEventAsset(rootNode:identifier:), passing in a unique identifier you define for the subclass.The particular configuration you choose for a node hierarchy instructs PHASE on which audio to play, when to play it, or whether to hand off an invocation to one or more child nodes (children).For example, if you register and invoke a PHASESwitchNodeDefinition that contains two child PHASESamplerNodeDefinition objects, PHASE plays the audio of one of the child sampler nodes based on the current value of the switch node’s metaparameter. For more information, see metaParameters.TopicsAccessing Child Nodesvar children: [PHASESoundEventNodeDefinition]An array of child sound event nodes.Identifying a Definitionclass PHASEDefinitionA base class that adds a name to framework definitions.RelationshipsInherits FromPHASEDefinitionInherited ByPHASEBlendNodeDefinitionPHASEContainerNodeDefinitionPHASEGeneratorNodeDefinitionPHASERandomNodeDefinitionPHASESwitchNodeDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoAudio Selection and Playbackclass PHASESoundAssetA sound resource stored in the asset registry.class PHASESoundEventAn object that determines which audio to play.enum RenderingStateThe playback status of audio.class PHASESoundEventNodeAssetA template object for sounds that can play in reaction to environmental state.class PHASEAssetA base class that adds a name to framework assets.API ReferenceSound Event NodesObjects that connect to form a hierarchical tree of audio actions.

### children | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesoundeventnodedefinition/children

PHASE  PHASESoundEventNodeDefinition  children Instance PropertychildrenAn array of child sound event nodes.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var children: [PHASESoundEventNodeDefinition] { get }DiscussionTo add children, use the add subtree functions of the derived class. For example, add children to a container node using addSubtree(_:).

## PHASESource | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesource

PHASE  PHASESource ClassPHASESourceAn object that plays audio from a 3D location and orientation in a scene.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASESource Mentioned in  Playing sound from a location in a 3D scene OverviewThis class represents a sound-emitting point or area in a virtual environment, positioned and oriented by a 3D transform.A spatial mixer, PHASESpatialMixerDefinition, adds environmental effects to sound sources. To tie a mixer to a sound source, create a PHASEMixerParameters object and pass it into the mixerParameters argument of a sound event’s init(engine:assetIdentifier:mixerParameters:) initializer.For an example that demonstrates sound sources, see Playing sound from a location in a 3D scene.TopicsCreating a Sourceinit(engine: PHASEEngine)Creates a single point in the environment from which sound emanates.init(engine: PHASEEngine, shapes: [PHASEShape])Creates a voluminous area in the environment from which sound emanates.Controlling Sound Volumevar gain: DoubleThe amount of sound the source emanates.Inspecting the Shapevar shapes: [PHASEShape]An array of shapes that collectively define the audio-emitting surface area of a volumetric source.RelationshipsInherits FromPHASEObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSCopyingNSObjectProtocolSee AlsoSoundscape Creationclass PHASEListenerA central point of reference that defines the location within the scene that’s most audible to the user.class PHASEOccluderAn object with a shape and position that blocks audio from reaching the listener.class PHASEObjectAn object in the scene.class PHASEShapeA collection of points that connect to form a 3D volume.class ElementAn object that describes the characteristics of a physical surface.class PHASEMaterialSurface characteristics that determine the acoustic properties of an object.enum PHASEMaterialPresetA collection of physical surfaces that each add a unique acoustic quality to your app’s audio.class PHASEMixerParametersAn object that specifies a mixer for sound events and orients them in 3D space.

### gain | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesource/gain

PHASE  PHASESource  gain Instance PropertygainThe amount of sound the source emanates.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var gain: Double { get set }DiscussionThe framework clamps the value to the range between 0 and 1, where 0 silences the audio and 1 doesn’t modify the audio’s original volume.

### init(engine:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesource/init(engine:)

PHASE  PHASESource  init(engine:) Initializerinit(engine:)Creates a single point in the environment from which sound emanates.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(engine: PHASEEngine) Parameters engineThe object that controls this class’ associated audio output.See AlsoCreating a Sourceinit(engine: PHASEEngine, shapes: [PHASEShape])Creates a voluminous area in the environment from which sound emanates.

### init(engine:shapes:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesource/init(engine:shapes:)

PHASE  PHASESource  init(engine:shapes:) Initializerinit(engine:shapes:)Creates a voluminous area in the environment from which sound emanates.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(
    engine: PHASEEngine,
    shapes: [PHASEShape]
) Parameters engineThe object that controls this class’ associated audio output.shapesA list of volumes that emanate sound.See AlsoCreating a Sourceinit(engine: PHASEEngine)Creates a single point in the environment from which sound emanates.

### shapes | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasesource/shapes

PHASE  PHASESource  shapes Instance PropertyshapesAn array of shapes that collectively define the audio-emitting surface area of a volumetric source.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var shapes: [PHASEShape] { get }DiscussionThe framework sets the contents to the shapes argument of the init(engine:shapes:) initializer.

## PHASESpatialCategory | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialcategory

PHASE  PHASESpatialCategory StructurePHASESpatialCategorySound resonance effects for spatial mixing.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+struct PHASESpatialCategoryDiscussionThis class identifies the various audio layers that a spatial mixer offers as keys to the entries dictionary.TopicsCreating a Spatial Categoryinit(rawValue: String)Initializes a spatial category with the given string.Categoriesstatic let directPathTransmission: PHASESpatialCategoryA spatial category that refers to the unfiltered audio signal.static let earlyReflections: PHASESpatialCategoryA spatial category that refers to the earlier echoes along the duration of sound resonance.static let lateReverb: PHASESpatialCategoryA spatial category that refers to the later echoes along the duration of sound resonance.RelationshipsConforms ToEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoSound Reflections and Resonanceclass PHASESpatialPipelineAn object that specifies the volume of optional environmental effects.class PHASESpatialPipelineEntryAn audio layer with an adjustable volume for a spatial mixer’s output.struct FlagsSound resonance options for a spatial pipeline.

### directPathTransmission | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialcategory/directpathtransmission

PHASE  PHASESpatialCategory  directPathTransmission Type PropertydirectPathTransmissionA spatial category that refers to the unfiltered audio signal.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static let directPathTransmission: PHASESpatialCategorySee AlsoCategoriesstatic let earlyReflections: PHASESpatialCategoryA spatial category that refers to the earlier echoes along the duration of sound resonance.static let lateReverb: PHASESpatialCategoryA spatial category that refers to the later echoes along the duration of sound resonance.

### earlyReflections | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialcategory/earlyreflections

PHASE  PHASESpatialCategory  earlyReflections Type PropertyearlyReflectionsA spatial category that refers to the earlier echoes along the duration of sound resonance.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static let earlyReflections: PHASESpatialCategorySee AlsoCategoriesstatic let directPathTransmission: PHASESpatialCategoryA spatial category that refers to the unfiltered audio signal.static let lateReverb: PHASESpatialCategoryA spatial category that refers to the later echoes along the duration of sound resonance.

### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialcategory/init(rawvalue:)

PHASE  PHASESpatialCategory  init(rawValue:) Initializerinit(rawValue:)Initializes a spatial category with the given string.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init(rawValue: String) Parameters rawValueThe enumeration case’s underlying string value.DiscussionTo initialize a spatial category:// Set the raw-value variable to the `directPathTransmission` constant. 
var rawValue: String = PHASESpatialCategoryDirectPathTransmission
var spatialPipelineOption = PHASESpatialCategory(rawValue: rawValue)
To check a spatial category’s raw value, see the Objective-C declaration of the struct member.

### lateReverb | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialcategory/latereverb

PHASE  PHASESpatialCategory  lateReverb Type PropertylateReverbA spatial category that refers to the later echoes along the duration of sound resonance.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static let lateReverb: PHASESpatialCategorySee AlsoCategoriesstatic let directPathTransmission: PHASESpatialCategoryA spatial category that refers to the unfiltered audio signal.static let earlyReflections: PHASESpatialCategoryA spatial category that refers to the earlier echoes along the duration of sound resonance.

## PHASESpatializationMode | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatializationmode

PHASE  PHASESpatializationMode EnumerationPHASESpatializationModeThe manner in which PHASE outputs spatial audio.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+enum PHASESpatializationModeOverviewWhen your app outputs audio through a spatial mixer, PHASESpatialMixerDefinition, the PHASE engine requires your app to choose an option of this enumeration and assign it to the outputSpatializationMode property.TopicsModescase automaticA mode that indicates that the framework chooses the spatialization mode.case alwaysUseBinauralA mode that introduces special processing to replicate a realistic spatial listening experience.case alwaysUseChannelBasedA mode that adds a 3D position and orientation to sound by panning across the available output channels.Initializersinit?(rawValue: Int)RelationshipsConforms ToBitwiseCopyableEquatableHashableRawRepresentableSendableSendableMetatypeSee AlsoSetupclass PHASEEngineAn object that manages audio assets, controls playback, and configures environmental effects.enum UpdateModeModes that determine when the framework consumes API calls and updates internal state.enum RenderingModeModes that determine whether the system renders audio in process or out of process.Betaclass PHASEAssetRegistryA central repository of audio assets.enum PHASENormalizationModeOptions that determine whether the framework adjusts a sound asset’s loudness for the user’s output device.enum PHASEReverbPresetThe manner in which PHASE diffuses resonating sound.class PHASEMediumA property or quality of the environment that affects how sound travels.

### PHASESpatializationMode.alwaysUseBinaural | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatializationmode/alwaysusebinaural

PHASE  PHASESpatializationMode  PHASESpatializationMode.alwaysUseBinaural CasePHASESpatializationMode.alwaysUseBinauralA mode that introduces special processing to replicate a realistic spatial listening experience.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case alwaysUseBinauralDiscussionEnable this mode to override a system or user preference and implement binaural audio output. When binaural mode plays through internal speakers on supported Apple devices, the framework applies additional effects to the output to achieve a sound experience comparable to one with headphones.See AlsoModescase automaticA mode that indicates that the framework chooses the spatialization mode.case alwaysUseChannelBasedA mode that adds a 3D position and orientation to sound by panning across the available output channels.

### PHASESpatializationMode.alwaysUseChannelBased | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatializationmode/alwaysusechannelbased

PHASE  PHASESpatializationMode  PHASESpatializationMode.alwaysUseChannelBased CasePHASESpatializationMode.alwaysUseChannelBasedA mode that adds a 3D position and orientation to sound by panning across the available output channels.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case alwaysUseChannelBasedDiscussionThe framework selects a channel layout for the output audio that’s compatible with the device’s channel configuration in Settings.This mode applies the same effect regardless of the current output device.See AlsoModescase automaticA mode that indicates that the framework chooses the spatialization mode.case alwaysUseBinauralA mode that introduces special processing to replicate a realistic spatial listening experience.

### PHASESpatializationMode.automatic | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatializationmode/automatic

PHASE  PHASESpatializationMode  PHASESpatializationMode.automatic CasePHASESpatializationMode.automaticA mode that indicates that the framework chooses the spatialization mode.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+case automaticDiscussionThis setting instructs the framework to automatically set a mode that determines how PHASE positions and orients sound in 3D space. The framework chooses a mode based on the output device:PHASESpatializationMode.binauralHeadphones (Bluetooth or line output) and the internal speakers of supported Mac or iOS devices.PHASESpatializationMode.channelBasedExternal speakers with 2 or more channels.See AlsoModescase alwaysUseBinauralA mode that introduces special processing to replicate a realistic spatial listening experience.case alwaysUseChannelBasedA mode that adds a 3D position and orientation to sound by panning across the available output channels.

### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatializationmode/init(rawvalue:)

PHASE  PHASESpatializationMode  init(rawValue:) Initializerinit(rawValue:)iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init?(rawValue: Int)

## PHASESpatialMixerDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialmixerdefinition

PHASE  PHASESpatialMixerDefinition ClassPHASESpatialMixerDefinitionAn audio-layering object that produces environmental effects and plays sound with a 3D position and orientation.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASESpatialMixerDefinition Mentioned in  Playing sound from a location in a 3D scene OverviewThis class enables the app to define a relationship between a source and listener in six degrees of freedom: orientation (roll, pitch, yaw) and a 3D position (x, y, z).The framework plays back an audio source with distance modeling (see distanceModelParameters), direct path transmission effects and any combination of environmental effects, such as reverb (see PHASESpatialPipeline), and directivity (see listenerDirectivityModelParameters). The result enables an app to implement directive point or omnidirectional sound sources — with or without direction, respectively — and volumetric sources with a defined shape.For a walkthrough of spatial mixing, see Playing sound from a location in a 3D scene.TopicsCreating a Spatial Mixerinit(spatialPipeline: PHASESpatialPipeline)Creates a mixer with the designated spatial pipeline.convenience init(spatialPipeline: PHASESpatialPipeline, identifier: String)Creates a named mixer with the designated spatial pipeline.Setting a Pipelinevar spatialPipeline: PHASESpatialPipelineAn object that adds sound layers for environmental effects.Changing Sound Over Distancevar distanceModelParameters: PHASEDistanceModelParameters?An effect that changes sound as it carries over a distance.Configuring Directivityvar listenerDirectivityModelParameters: PHASEDirectivityModelParameters?A data set that determines how well the listener hears depending on its direction relative to a sound source.var sourceDirectivityModelParameters: PHASEDirectivityModelParameters?A data set that directs sound such that it’s louder when directed at the listener.RelationshipsInherits FromPHASEMixerDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocol

### distanceModelParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialmixerdefinition/distancemodelparameters

PHASE  PHASESpatialMixerDefinition  distanceModelParameters Instance PropertydistanceModelParametersAn effect that changes sound as it carries over a distance.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var distanceModelParameters: PHASEDistanceModelParameters? { get set }DiscussionSimilar to a Doppler effect, this property changes how an audio source sounds as its distance between the listener increases or decreases in 3D space. The available options are:PHASEGeometricSpreadingDistanceModelParametersCreate a realistic effect by dissipating certain frequency ranges of the audio spectrum differently with distance.PHASEEnvelopeDistanceModelParametersTake full control of the sound’s volume by graphing its loudness using points and curves over the distance.Programmatically Check Sound DissipationAfter setting a value for this property, you can move a looping sound source to tweak the effect to your app’s particular requirements. The following code programmaticaly moves a looping source away from the listener along the z-axis:spatialSamplerNode.playbackType = PHASEPlaybackType.looping
// ... 
var sourceTransform: PHASETransform3D = origin
sourceTransform.columns.3.z -= 6.0
while (true) {
    var posToSet: PHASETransform3D = source.transform
    posToSet.columns.3.z -= 0.05
    if (posToSet.columns.3.z < -20.0)
    {
        posToSet.columns.3.z = -6.0;
    }
    source.transform = posToSet
    usleep(20000) // 20 ms
    print("z =", source.transform.columns.3.z);
}     
spatialSamplerNode.playbackType = PHASEPlaybackTypeLooping;
// ...
PHASETransform3D sourceTransform = origin;
sourceTransform.columns[3].z -= 6.f;
while (1) {
    PHASETransform3D posToSet = _source.transform;
    posToSet.columns[3].z -= .05f;
    if (posToSet.columns[3].z < -20.f)
    {
        posToSet.columns[3].z = -6.f;
    }
    _source.transform = posToSet;
    [NSThread sleepForTimeInterval:.02f]; // 20 ms
    NSLog(@"z = %f", _source.transform.columns[3].z);
}

### init(spatialPipeline:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialmixerdefinition/init(spatialpipeline:)

PHASE  PHASESpatialMixerDefinition  init(spatialPipeline:) Initializerinit(spatialPipeline:)Creates a mixer with the designated spatial pipeline.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(spatialPipeline: PHASESpatialPipeline) Parameters spatialPipelineAn object that features optional environmental effects.See AlsoCreating a Spatial Mixerconvenience init(spatialPipeline: PHASESpatialPipeline, identifier: String)Creates a named mixer with the designated spatial pipeline.

### init(spatialPipeline:identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialmixerdefinition/init(spatialpipeline:identifier:)

PHASE  PHASESpatialMixerDefinition  init(spatialPipeline:identifier:) Initializerinit(spatialPipeline:identifier:)Creates a named mixer with the designated spatial pipeline.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+convenience init(
    spatialPipeline: PHASESpatialPipeline,
    identifier: String
) Parameters spatialPipelineAn object that features optional sound resonance effects.identifierA unique name for the spatial mixer.See AlsoCreating a Spatial Mixerinit(spatialPipeline: PHASESpatialPipeline)Creates a mixer with the designated spatial pipeline.

### listenerDirectivityModelParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialmixerdefinition/listenerdirectivitymodelparameters

PHASE  PHASESpatialMixerDefinition  listenerDirectivityModelParameters Instance PropertylistenerDirectivityModelParametersA data set that determines how well the listener hears depending on its direction relative to a sound source.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var listenerDirectivityModelParameters: PHASEDirectivityModelParameters? { get set }DiscussionAn app can configure this property to attenuate sound to the sides of the listener while leaving sound in front of or behind the listener unchanged.See AlsoConfiguring Directivityvar sourceDirectivityModelParameters: PHASEDirectivityModelParameters?A data set that directs sound such that it’s louder when directed at the listener.

### sourceDirectivityModelParameters | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialmixerdefinition/sourcedirectivitymodelparameters

PHASE  PHASESpatialMixerDefinition  sourceDirectivityModelParameters Instance PropertysourceDirectivityModelParametersA data set that directs sound such that it’s louder when directed at the listener.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var sourceDirectivityModelParameters: PHASEDirectivityModelParameters? { get set }DiscussionThe framework applies directivity to sound sources that emanate from a point.See AlsoConfiguring Directivityvar listenerDirectivityModelParameters: PHASEDirectivityModelParameters?A data set that determines how well the listener hears depending on its direction relative to a sound source.

### spatialPipeline | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialmixerdefinition/spatialpipeline

PHASE  PHASESpatialMixerDefinition  spatialPipeline Instance PropertyspatialPipelineAn object that adds sound layers for environmental effects.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var spatialPipeline: PHASESpatialPipeline { get }DiscussionThe framework sets the value to the spatialPipeline initializer argument. See init(spatialPipeline:).

## PHASESpatialPipeline | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialpipeline

PHASE  PHASESpatialPipeline ClassPHASESpatialPipelineAn object that specifies the volume of optional environmental effects.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASESpatialPipelineOverviewThe PHASESpatialMixerDefinition class contains an instance of this class, spatialPipeline, to add optional sound layers to the output.On top of the original audio signal designated by directPathTransmission, this class optionally includes audio layers for environmental effects, such as earlyReflections or lateReverb, in the output.  To control the amount of volume that either audio layer possesses in the mixer’s output, adjust the sendLevel for the layer’s respective PHASESpatialPipelineEntry member in the entries dictionary.TopicsCreating a Spatial Pipelineinit?(flags: PHASESpatialPipeline.Flags)Creates a spatial pipeline with the specified flags.struct FlagsSound resonance options for a spatial pipeline.Inspecting Effectsvar flags: PHASESpatialPipeline.FlagsA collection of environmental effects to include in the output.var entries: [PHASESpatialCategory : PHASESpatialPipelineEntry]Audio layers for environmental effects to add to the output.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSound Reflections and Resonanceclass PHASESpatialPipelineEntryAn audio layer with an adjustable volume for a spatial mixer’s output.struct PHASESpatialCategorySound resonance effects for spatial mixing.struct FlagsSound resonance options for a spatial pipeline.

### entries | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialpipeline/entries

PHASE  PHASESpatialPipeline  entries Instance PropertyentriesAudio layers for environmental effects to add to the output.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var entries: [PHASESpatialCategory : PHASESpatialPipelineEntry] { get }DiscussionThis property includes an entry for each spatial category that the app includes in the init(flags:) argument. Adjust an entry’s send level to blend its audio layer into the output signal. For example, by fading the input audio signal using the sendLevelMetaParameterDefinition property of the directPathTransmission entry, the app can lower the dry signal and blend in the right balance of early reflections and reverb.See AlsoInspecting Effectsvar flags: PHASESpatialPipeline.FlagsA collection of environmental effects to include in the output.

### flags | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialpipeline/flags-swift.property

PHASE  PHASESpatialPipeline  flags Instance PropertyflagsA collection of environmental effects to include in the output.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var flags: PHASESpatialPipeline.Flags { get }DiscussionThe framework sets the value of this property to the init(flags:) argument.See AlsoInspecting Effectsvar entries: [PHASESpatialCategory : PHASESpatialPipelineEntry]Audio layers for environmental effects to add to the output.

### PHASESpatialPipeline.Flags | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialpipeline/flags-swift.struct

PHASE  PHASESpatialPipeline  PHASESpatialPipeline.Flags StructurePHASESpatialPipeline.FlagsSound resonance options for a spatial pipeline.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+struct FlagsOverviewEach PHASESpatialPipeline specifies a flag in its init(flags:) initializer.TopicsCreating a Flaginit(rawValue: UInt)Initializes a spatial flag with the given string.Choosing a Flagstatic var directPathTransmission: PHASESpatialPipeline.FlagsA spatial property that refers to the original audio signal.static var earlyReflections: PHASESpatialPipeline.FlagsA spatial property that refers to the earlier echoes along the duration of sound resonance.static var lateReverb: PHASESpatialPipeline.FlagsA spatial property that refers to the later echoes along the duration of sound resonance.RelationshipsConforms ToBitwiseCopyableEquatableExpressibleByArrayLiteralOptionSetRawRepresentableSendableSendableMetatypeSetAlgebraSee AlsoSound Reflections and Resonanceclass PHASESpatialPipelineAn object that specifies the volume of optional environmental effects.class PHASESpatialPipelineEntryAn audio layer with an adjustable volume for a spatial mixer’s output.struct PHASESpatialCategorySound resonance effects for spatial mixing.

#### directPathTransmission | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialpipeline/flags-swift.struct/directpathtransmission

PHASE  PHASESpatialPipeline  PHASESpatialPipeline  PHASESpatialPipeline.Flags  directPathTransmission Type PropertydirectPathTransmissionA spatial property that refers to the original audio signal.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var directPathTransmission: PHASESpatialPipeline.Flags { get } Mentioned in  Playing sound from a location in a 3D scene See AlsoChoosing a Flagstatic var earlyReflections: PHASESpatialPipeline.FlagsA spatial property that refers to the earlier echoes along the duration of sound resonance.static var lateReverb: PHASESpatialPipeline.FlagsA spatial property that refers to the later echoes along the duration of sound resonance.

#### earlyReflections | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialpipeline/flags-swift.struct/earlyreflections

PHASE  PHASESpatialPipeline  PHASESpatialPipeline  PHASESpatialPipeline.Flags  earlyReflections Type PropertyearlyReflectionsA spatial property that refers to the earlier echoes along the duration of sound resonance.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var earlyReflections: PHASESpatialPipeline.Flags { get } Mentioned in  Playing sound from a location in a 3D scene See AlsoChoosing a Flagstatic var directPathTransmission: PHASESpatialPipeline.FlagsA spatial property that refers to the original audio signal.static var lateReverb: PHASESpatialPipeline.FlagsA spatial property that refers to the later echoes along the duration of sound resonance.

#### init(rawValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialpipeline/flags-swift.struct/init(rawvalue:)

PHASE  PHASESpatialPipeline  PHASESpatialPipeline  PHASESpatialPipeline.Flags  init(rawValue:) Initializerinit(rawValue:)Initializes a spatial flag with the given string.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+init(rawValue: UInt) Parameters rawValueThe enumeration case’s underlying string value.

#### lateReverb | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialpipeline/flags-swift.struct/latereverb

PHASE  PHASESpatialPipeline  PHASESpatialPipeline  PHASESpatialPipeline.Flags  lateReverb Type PropertylateReverbA spatial property that refers to the later echoes along the duration of sound resonance.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+static var lateReverb: PHASESpatialPipeline.Flags { get } Mentioned in  Playing sound from a location in a 3D scene See AlsoChoosing a Flagstatic var directPathTransmission: PHASESpatialPipeline.FlagsA spatial property that refers to the original audio signal.static var earlyReflections: PHASESpatialPipeline.FlagsA spatial property that refers to the earlier echoes along the duration of sound resonance.

### init(flags:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialpipeline/init(flags:)

PHASE  PHASESpatialPipeline  init(flags:) Initializerinit(flags:)Creates a spatial pipeline with the specified flags.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init?(flags: PHASESpatialPipeline.Flags) Parameters flagsAn array of sound-resonance effects to include in the spatial pipeline’s output. The framework adds an entry to the entries property for each element that the app includes in this collection.DiscussionThis initializer returns nil for a nil flags argument.See AlsoCreating a Spatial Pipelinestruct FlagsSound resonance options for a spatial pipeline.

## PHASESpatialPipelineEntry | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialpipelineentry

PHASE  PHASESpatialPipelineEntry ClassPHASESpatialPipelineEntryAn audio layer with an adjustable volume for a spatial mixer’s output.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASESpatialPipelineEntryOverviewThis property adjusts the amount of audio that passes through a spatial mixer’s pipeline (spatialPipeline) to the output. The pipeline’s entries contains an instance of this class for each type of audio layer that PHASESpatialCategory defines. Depending on the layer’s type, the audio may sound like spatial relections, environmental reverb, or the unfiltered signal. An app adjusts the layer’s presence in the mixer’s output by:Defining an initial volume using sendLevelAdjusting the audio’s volume dynamically, for example, by fading it over a duration using sendLevelMetaParameterDefinitionTopicsSetting the Send Levelvar sendLevel: DoubleThe amount of audio signal to add to the output.Fading the Send Levelvar sendLevelMetaParameterDefinition: PHASENumberMetaParameterDefinition?A parameter that gradually updates the amount of audio signal that passes through to the output.RelationshipsInherits FromNSObjectConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoSound Reflections and Resonanceclass PHASESpatialPipelineAn object that specifies the volume of optional environmental effects.struct PHASESpatialCategorySound resonance effects for spatial mixing.struct FlagsSound resonance options for a spatial pipeline.

### sendLevel | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialpipelineentry/sendlevel

PHASE  PHASESpatialPipelineEntry  sendLevel Instance PropertysendLevelThe amount of audio signal to add to the output.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var sendLevel: Double { get set }DiscussionThe framework clamps the value to the range between 0 and 1, where 0 silences the audio and 1 passes the audio through to the output at full volume. The default value is 1.When an app adds the entry’s spatial pipeline (see entries) to a sound event, the framework observes no further adjustments to this property. To change the send level after that, adjust the sendLevelMetaParameterDefinition.

### sendLevelMetaParameterDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasespatialpipelineentry/sendlevelmetaparameterdefinition

PHASE  PHASESpatialPipelineEntry  sendLevelMetaParameterDefinition Instance PropertysendLevelMetaParameterDefinitionA parameter that gradually updates the amount of audio signal that passes through to the output.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var sendLevelMetaParameterDefinition: PHASENumberMetaParameterDefinition? { get set }DiscussionUse this property to fade reverb effects into a spatial mixer’s output.For example, to begin with no reverb and gradually enable it, start by silencing reverb by setting the lateReverb entry’s sendLevel to 0. Begin the fade by calling fade(value:duration:) on this property with an argument of 1.

## PHASEStreamNode | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasestreamnode

PHASE  PHASEStreamNode ClassPHASEStreamNodeiOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 2.0+class PHASEStreamNodeOverviewThe base class for stream nodes, exposing common elements.TopicsInstance Propertiesvar format: AVAudioFormatvar gainMetaParameter: PHASENumberMetaParameter?var mixer: PHASEMixervar rateMetaParameter: PHASENumberMetaParameter?RelationshipsInherits FromNSObjectInherited ByPHASEPullStreamNodePHASEPushStreamNodeConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocol

### format | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasestreamnode/format

PHASE  PHASEStreamNode  format Instance PropertyformatiOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 2.0+var format: AVAudioFormat { get }DiscussionThe readonly property that returns the AVAudioFormat that this stream was initialized with.

### gainMetaParameter | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasestreamnode/gainmetaparameter

PHASE  PHASEStreamNode  gainMetaParameter Instance PropertygainMetaParameteriOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 2.0+var gainMetaParameter: PHASENumberMetaParameter? { get }DiscussionIf specified during construction, the metaparameter for controlling gain will be available here

### mixer | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasestreamnode/mixer

PHASE  PHASEStreamNode  mixer Instance PropertymixeriOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 2.0+var mixer: PHASEMixer { get }DiscussionThe readonly property that returns the PHASEMixer this stream was created with and assigned to.

### rateMetaParameter | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasestreamnode/ratemetaparameter

PHASE  PHASEStreamNode  rateMetaParameter Instance PropertyrateMetaParameteriOS 18.0+iPadOS 18.0+Mac Catalyst 18.0+macOS 15.0+tvOS 18.0+visionOS 2.0+var rateMetaParameter: PHASENumberMetaParameter? { get }DiscussionIf specified during construction, the metaparameter for controlling rate/pitch will be available here

## PHASEStringMetaParameter | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasestringmetaparameter

PHASE  PHASEStringMetaParameter ClassPHASEStringMetaParameterA metaparameter with a text definition that can change over time.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEStringMetaParameterOverviewThis class contains text that updates, like a “weather” metaparameter that the app changes from “rainy” to “sunny.”To create an instance of this class, first create a PHASEStringMetaParameterDefinition, and either:Register it with the engine by calling registerGlobalMetaParameter(metaParameterDefinition:), then access the instance of this class in the engine’s globalMetaParameters dictionary.Pass it to the PHASESwitchNodeDefinition initializer, init(switchMetaParameterDefinition:), and then access the instance of this class in a sound event’s metaParameters dictionary.RelationshipsInherits FromPHASEMetaParameterConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoTextual Metaparametersclass PHASEStringMetaParameterDefinitionA specification for a metaparameter defined by text.

## PHASEStringMetaParameterDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasestringmetaparameterdefinition

PHASE  PHASEStringMetaParameterDefinition ClassPHASEStringMetaParameterDefinitionA specification for a metaparameter defined by text.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASEStringMetaParameterDefinitionOverviewUse this class to spawn discrete instances of PHASENumberMetaParameter, for example, a “player speed” metaparameter that the app changes gradually from 0.0 to 1.0.To use a number metaparameter, create an instance of this class and:Register it with the engine by calling registerGlobalMetaParameter(metaParameterDefinition:), then access the instance of this class in the engine’s globalMetaParameters dictionary.Pass it to the PHASEBlendNodeDefinition initializer, init(blendMetaParameterDefinition:identifier:), and then access the instance of this class in a sound event’s metaParameters dictionary.TopicsCreating a Parameter Definitioninit(value: String)Creates a specification for a textual metaparameter with the given value.convenience init(value: String, identifier: String)Creates a specification for a named textual metaparameter with the given value.RelationshipsInherits FromPHASEMetaParameterDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoTextual Metaparametersclass PHASEStringMetaParameterA metaparameter with a text definition that can change over time.

### init(value:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasestringmetaparameterdefinition/init(value:)

PHASE  PHASEStringMetaParameterDefinition  init(value:) Initializerinit(value:)Creates a specification for a textual metaparameter with the given value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(value: String) Parameters valueThe default text for the metaparameter specification.See AlsoCreating a Parameter Definitionconvenience init(value: String, identifier: String)Creates a specification for a named textual metaparameter with the given value.

### init(value:identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phasestringmetaparameterdefinition/init(value:identifier:)

PHASE  PHASEStringMetaParameterDefinition  init(value:identifier:) Initializerinit(value:identifier:)Creates a specification for a named textual metaparameter with the given value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+convenience init(
    value: String,
    identifier: String
) Parameters valueThe default text for the metaparameter specification.identifierA unique name for the metaparameter specification.See AlsoCreating a Parameter Definitioninit(value: String)Creates a specification for a textual metaparameter with the given value.

## PHASESwitchNodeDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseswitchnodedefinition

PHASE  PHASESwitchNodeDefinition ClassPHASESwitchNodeDefinitionA node that passes invocation to only one of its child nodes.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+class PHASESwitchNodeDefinitionOverviewA switch node takes a different path in a sound-event hierarchy depending on the value that the app supplies for the node’s switch metaparameter. You define the available paths ahead of time by calling addSubtree(_:switchValue:) at least twice and supplying the subtree’s unique string name as the switch value. When your app invokes a sound event at runtime, PHASE checks the value of switchMetaParameterDefinition to determine which path to take.Switch Between Mulitple Node TreesFor example, the following diagram represents a node tree that plays one of three grass or sidewalk footstep sounds, depending on the app’s current state. The app sets a value for the switch-node metaparameter according to the terrain on which the player in a game currently stands.The following code creates a random node subtree for each terrain type and adds each one as a subtree to the switch node.// Set up the sampler nodes for the "grass" group of sounds.
let grassFootstep1 = PHASESamplerNodeDefinition(soundAssetIdentifier:"GrassOne" , mixerDefinition: myMixer)
let grassFootstep2 = PHASESamplerNodeDefinition(soundAssetIdentifier:"GrassTwo" , mixerDefinition: myMixer)

// Create a random node and assign the grass samplers to it.
let grassRandomNode = PHASERandomNodeDefinition(identifier: "grassRandomNode")
grassRandomNode.addSubtree(grassFootstep1, weight: 10)
grassRandomNode.addSubtree(grassFootstep2, weight: 5)

// Set up the sampler nodes for the "cobblestone" group of sounds.
let cobblestoneFootstep1 = PHASESamplerNodeDefinition(soundAssetIdentifier: "CobblestoneOne", mixerDefinition: myMixer)
let cobblestoneFootstep2 = PHASESamplerNodeDefinition(soundAssetIdentifier: "CobblestoneTwo", mixerDefinition: myMixer)

// Create a random node and assign the cobblestone samplers to it.
let cobblestoneRandomNode = PHASERandomNodeDefinition(identifier: "cobblestoneRandomNode")
cobblestoneRandomNode.addSubtree(cobblestoneFootstep1, weight: 4)
cobblestoneRandomNode.addSubtree(cobblestoneFootstep2, weight: 2)

// Create a metaparameter definition named "terrain" for the sound event.
let terrainSwitchParameter = PHASEStringMetaParameterDefinition(value: "cobblestone", identifier:"terrain")

// Create a switch node and provide the metaparameter.
let terrainSwitchNode = PHASESwitchNodeDefinition(switchMetaParameterDefinition: terrainSwitchParameter)

// Add two random nodes as the metaparameter toggle options.
terrainSwitchNode.addSubtree(cobblestoneRandomNode, switchValue: "cobblestone")
terrainSwitchNode.addSubtree(grassRandomNode, switchValue: "grass")

// Set the terrain metaparameter to play the sound event.
var footstepEvent: PHASESoundEvent!
do {
    footstepEvent = try PHASESoundEvent(engine: myEngine, assetIdentifier: "footStepEventAsset")
} catch { fatalError("Failed to create sound event.") }

// Set the terrain to grass.
if let metaparameter = footstepEvent.metaParameters["terrain"] {
    metaparameter.value = "grass"
}

// Invoke the sound event and hear noise for the selected terrain.
footstepEvent.start()
// Set up the sampler nodes for the "grass" group of sounds.
PHASESamplerNodeDefinition* grassFootstep1 = [[PHASESamplerNodeDefinition alloc] 
    initWithSoundAssetUID:@"GrassOne" mixerDefinition:mixNode];
PHASESamplerNodeDefinition* grassFootstep2 = [[PHASESamplerNodeDefinition alloc] 
    initWithSoundAssetUID:@"GrassTwo" mixerDefinition:mixNode];

// Create a random node and assign the grass samplers to it.
PHASERandomNodeDefinition* grassRandomNode = [[PHASERandomNodeDefinition alloc] 
    initWithUID:@"grassRandomNode"];
[grassRandomNode addSubtree:grassFootstep1 weight:@10];
[grassRandomNode addSubtree:grassFootstep2 weight:@5];

// Set up the sampler nodes for the "cobblestone" group of sounds.
PHASESamplerNodeDefinition* cobblestoneFootstep1 = [[PHASESamplerNodeDefinition alloc] 
    initWithSoundAssetUID:@"CobblestoneOne" mixerDefinition:mixNode];
PHASESamplerNodeDefinition* cobblestoneFootstep2 = [[PHASESamplerNodeDefinition alloc] 
    initWithSoundAssetUID:@"CobblestoneTwo" mixerDefinition:mixNode];

// Create a random node and assign the cobblestone samplers to it.
PHASERandomNodeDefinition* cobblestoneRandomNode = [[PHASERandomNodeDefinition alloc] 
    initWithUID:@"cobblestoneRandomNode"];
[cobblestoneRandomNode addSubtree:cobblestoneFootstep1 weight:@4];
[cobblestoneRandomNode addSubtree:cobblestoneFootstep2 weight:@2];

// Create a metaparameter definition named "terrain" for the sound event.
PHASEStringMetaParameterDefinition terrainSwitchParameter = 
    [[PHASEStringMetaParameterDefinition alloc] 
        initWithValue:@"cobblestone" uid:@"terrain"];

// Create a switch node and provide the metaparameter.
PHASESwitchNodeDefinition* terrainSwitchNode = [[PHASESwitchNodeDefinition alloc] 
    initWithSwitchMetaParameterDefinition:terrainSwitchParameter];

// Add two random nodes as the metaparameter toggle options.
[terrainSwitchNode addSubtree:cobblestoneRandomNode switchValue:@"cobblestone"];
[terrainSwitchNode addSubtree:grassRandomNode switchValue:@"grass"];

// Set the terrain metaparameter to play the sound event.
PHASESoundEvent* footstepEvent = [[PHASESoundEvent alloc] 
    initWithEngine:_objects->mEngine
    registeredSoundEventNodeAssetUID:@"footStepEventAsset" outError:nil];

// Set the terrain to grass.
footstepEvent.metaParameters[@"terrain"] = @"grass";

// Invoke the sound event and hear noise for the selected terrain.
[footstepEvent startAndReturnError:&myError];
Tip The metaParameters objects affect only one sound event. To propagate a metaparameter change to multiple sound events, register the metaparameter globally using registerGlobalMetaParameter(metaParameterDefinition:), and change its value through the asset registry’s globalMetaParameters dictionary.TopicsCreating a Nodeinit(switchMetaParameterDefinition: PHASEStringMetaParameterDefinition)Creates a node that invokes a child node based on the value of the given parameter.convenience init(switchMetaParameterDefinition: PHASEStringMetaParameterDefinition, identifier: String)Creates a named node that invokes a child node based on the value of the given parameter.Managing Child Nodesvar switchMetaParameterDefinition: PHASEStringMetaParameterDefinitionThe meta parameter that holds the name of the child node to invoke.func addSubtree(PHASESoundEventNodeDefinition, switchValue: String)Adds a child node with the given switch value.RelationshipsInherits FromPHASESoundEventNodeDefinitionConforms ToCVarArgCustomDebugStringConvertibleCustomStringConvertibleEquatableHashableNSObjectProtocolSee AlsoControl Nodesclass PHASERandomNodeDefinitionA sound event node that invokes one of its child nodes at random.class PHASEBlendNodeDefinitionA node that smoothly fades between the audio of its child nodes.class PHASEContainerNodeDefinitionA node that plays all its children at the same time.

### addSubtree(_:switchValue:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseswitchnodedefinition/addsubtree(_:switchvalue:)

PHASE  PHASESwitchNodeDefinition  addSubtree(_:switchValue:) Instance MethodaddSubtree(_:switchValue:)Adds a child node with the given switch value.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+func addSubtree(
    _ subtree: PHASESoundEventNodeDefinition,
    switchValue: String
) Parameters subtreeThe child node, which itself can contain a hierarchical tree of descendent nodes.switchValueThe meta parameter value that invokes the subtree child node.See AlsoManaging Child Nodesvar switchMetaParameterDefinition: PHASEStringMetaParameterDefinitionThe meta parameter that holds the name of the child node to invoke.

### init(switchMetaParameterDefinition:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseswitchnodedefinition/init(switchmetaparameterdefinition:)

PHASE  PHASESwitchNodeDefinition  init(switchMetaParameterDefinition:) Initializerinit(switchMetaParameterDefinition:)Creates a node that invokes a child node based on the value of the given parameter.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+init(switchMetaParameterDefinition: PHASEStringMetaParameterDefinition) Parameters switchMetaParameterDefinitionA string meta parameter that specifies the child node identifier to pass invocation on to.See AlsoCreating a Nodeconvenience init(switchMetaParameterDefinition: PHASEStringMetaParameterDefinition, identifier: String)Creates a named node that invokes a child node based on the value of the given parameter.

### init(switchMetaParameterDefinition:identifier:) | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseswitchnodedefinition/init(switchmetaparameterdefinition:identifier:)

PHASE  PHASESwitchNodeDefinition  init(switchMetaParameterDefinition:identifier:) Initializerinit(switchMetaParameterDefinition:identifier:)Creates a named node that invokes a child node based on the value of the given parameter.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+convenience init(
    switchMetaParameterDefinition: PHASEStringMetaParameterDefinition,
    identifier: String
) Parameters switchMetaParameterDefinitionA string meta parameter that specifies the child node identifier to pass invocation on to.identifierA unique name for the switch node.See AlsoCreating a Nodeinit(switchMetaParameterDefinition: PHASEStringMetaParameterDefinition)Creates a node that invokes a child node based on the value of the given parameter.

### switchMetaParameterDefinition | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/phaseswitchnodedefinition/switchmetaparameterdefinition

PHASE  PHASESwitchNodeDefinition  switchMetaParameterDefinition Instance PropertyswitchMetaParameterDefinitionThe meta parameter that holds the name of the child node to invoke.iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 17.0+visionOS 1.0+var switchMetaParameterDefinition: PHASEStringMetaParameterDefinition { get }DiscussionThe framework sets the value of this property to the init(switchMetaParameterDefinition:) argument.See AlsoManaging Child Nodesfunc addSubtree(PHASESoundEventNodeDefinition, switchValue: String)Adds a child node with the given switch value.

## Playback Parameterization | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/playback-parameterization

Collection PHASE  Playback Parameterization API CollectionPlayback ParameterizationChange the characteristics of in-flight audio by adjusting its properties at runtime.OverviewMetaparameters control several features of a sound source or sound event, as they play back. For instance, metaparameters can adjust a switch node’s toggle, or the amount of reverb that a sound source emanates.Attach Metaparameters to a Particular SoundTo use a metaparameter, you attach it to a sound event or sound source. PHASE provides the following ways to attach metaparameters:PHASEGeneratorNodeDefinitiongainMetaParameterDefinition, rateMetaParameterDefinitionPHASEMixerDefinitiongainMetaParameterDefinitionPHASESwitchNodeDefinitioninit(switchMetaParameterDefinition:)PHASEBlendNodeDefinitioninit(blendMetaParameterDefinition:)PHASEMappedMetaParameterDefinitioninit(inputMetaParameterDefinition:envelope:identifier:)PHASESpatialPipelineEntrysendLevelMetaParameterDefinitionAdjust a Property of a Single Audio SignalThe framework refers to metaparameters that you access through a sound event’s metaParameters dictionary as local metaparameters. When you adjust the value of a local metaparameter, it affects just the sound event.The following code changes the volume on a specific sound event:// Create a `PHASEMetaParameterDefinition` instance.
let myGainParam = PHASENumberMetaParameterDefinition(value: 1, identifier: "gain")

// Create a sampler node that plays an audio file named "mySound".
let mySampler = PHASESamplerNodeDefinition(
    soundAssetIdentifier: "mySound",
    mixerDefinition: myMixer)

// Attach the metaparameter to the sampler node.
mySampler.gainMetaParameterDefinition = myGainParam;

// Invoke the sound event.
mySoundEvent.start()

// Access the local metaparameter and change the gain.
if let metaparameter = mySoundEvent.metaParameters["gain"] {
    metaparameter.value = 0.5
}
// Create a `PHASEMetaParameterDefinition` instance. 
PHASENumberMetaParameterDefinition* myGainParam = 
    [[PHASENumberMetaParameterDefinition alloc] 
    initWithValue:1 uid:@"gain"];

// Create a sampler node that plays an audio file named "mySound".
PHASESamplerNodeDefinition* mySampler = [[PHASESamplerNodeDefinition alloc]
    initWithSoundAssetUID:@"mySound"] mixerDefinition:myMixer];

// Attach the metaparameter to the sampler node.
mySampler.gainMetaParameterDefinition = myGainParam;

// Invoke the sound event.
[myPHASESoundEvent startAndReturnError:&myError];

// Access the local metaparameter and change the gain.
myPHASESoundEvent.metaParameters[@"gain"].value = 0.5
Share a Parameter with Multiple Audio SignalsThe framework refers to parameters that affect many sound events or sound sources as global metaparameters. Real-time adjustments to global metaparameters affect the playback of all sound events that initialize with the metaparameter.The following code changes a weather metaparameter for all of its associated sound events:// Create a `PHASEMetaParameterDefinition` instance.
let myGlobalWeatherParam = PHASEStringMetaParameterDefinition(
    value: "sunny", identifier: "weather")

// Register it as a global metaparameter.
do {
    try myEngine.assetRegistry.registerGlobalMetaParameter(metaParameterDefinition: myGlobalWeatherParam)
} catch {
    fatalError("Unable to register the weather metaparameter.")
}

// Attach it to a sound event node definition.
let mySwitchNode = PHASESwitchNodeDefinition(switchMetaParameterDefinition: myGlobalWeatherParam)

// Change the its value at runtime.
if let metaparameter = myEngine.assetRegistry.globalMetaParameters["weather"] {
    metaparameter.value = "rainy"
}
// Create a `PHASEMetaParameterDefinition` instance. 
PHASEStringMetaParameterDefinition* myGlobalWeatherParam = 
    [[PHASEStringMetaParameterDefinition alloc] 
    initWithValue:@"sunny" uid:@"weather"];

// Register it as a global metaparameter.
[myPHASEEngine.assetRegistry registerGlobalMetaParameter:myGlobalWeatherParam
    uid:@"weather"];

// Attach it to a sound event node definition.
PHASESwitchNodeDefinition* mySwitchNode = [[PHASESwitchNodeDefinition alloc] 
    initWithSwitchMetaParameterDefinition:myGlobalWeatherParam];

// Change the its value at runtime.
myPHASEEngine.assetRegistry.globalMetaParameters[@"weather"].value = @"rainy";
As part of the engine’s asset registry, the globalMetaParameters dictionary affects every playing sound event that shares a metaparameter that the dictionary contains.TopicsBase Metaparametersclass PHASEMetaParameterA named parameter with a value that the app can change over time.class PHASEMetaParameterDefinitionA specification for a named parameter with a constant value.class PHASEGlobalMetaParameterAssetA reference to a registered metaparameter that the app can share with multiple sound events or sources.Linear Metaparametersclass PHASENumberMetaParameterA metaparameter defined by a number that can change over time.class PHASENumberMetaParameterDefinitionA specification for a metaparameter defined by a number.Textual Metaparametersclass PHASEStringMetaParameterA metaparameter with a text definition that can change over time.class PHASEStringMetaParameterDefinitionA specification for a metaparameter defined by text.Graphed Metaparametersclass PHASEMappedMetaParameterDefinitionA metaparameter that graphs an input value on a set of mathematical curves.See AlsoDynamic Sound Controlclass PHASEEnvelopeA collection of segments that connect to graph a complex curve over a linear input.class PHASEEnvelopeSegmentA curved portion of an envelope.enum PHASECurveTypeOptions that apply a mathematical function to an input value.class PHASENumericPairAn ordered pair that defines a bounding box for an envelope.

## Playing sound from a location in a 3D scene | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/playing-sound-from-a-location-in-a-3d-scene

PHASE  Playing sound from a location in a 3D scene ArticlePlaying sound from a location in a 3D scenePosition sound from a specific direction and automatically raise or lower volume based on the environment.OverviewAudio that adjusts its volume based on distance to a specific reference point is called spatial audio. Spatial audio transmits sound from a particular location, or source, in a specific direction that you define by describing the sound’s 3D position and orientation. Your app can leverage spatial audio to define the point of reference, or define a listener as a player in a game. For example, to indicate that a horn resides on the left-hand side of a scene, PHASE outputs audio more through the left speaker.PHASE spatial audio accommodates a scene layout in several ways: by observing objects in the scene, the shape of the sound’s source, obstructions, and the point of reference of a listener. To complement obstacles and indoor locations in your scene, you can use spatial audio to layer environmental effects, for example, a reflection or reverberation, on top of spatial sounds.After describing your app’s scene, you queue sound to play by creating an event node asset that instructs PHASE on what to play and when. At runtime, PHASE checks your app’s state through the event node asset and plays sounds at the right moment that react in accordance to your app’s visual appearance.Set an object’s scene position and orientationBefore PHASE plays sound in 3D, you create several objects to model your app’s visual scene. Initialize and add the following classes to rootObject, the engine’s root object:PHASESource for sound sourcesPHASEListener for a listenerPHASEOccluder for optional occludersEach class derives from PHASEObject, which defines a transform to provide it with a unique 3D position and orientation in the scene.An app can define the scene as a level in a game that’s composed of a detailed set of visual properties, for example, textured pixel data, lighting, and animation. However, to play sound in accordance with the visual scene, PHASE only needs to know the scene’s geometric shape. PHASE interprets the shape through a tranform (of type simd_float4x4), and in particular, its array of four-column vectors. The following transform defines a zeroed orientation and position for a board-game piece:var chessPiecePose: simd_float4x4 = matrix_identity_float4x4
Define the location from which sound playsThe first type of object you define in the PHASE scene describes a location from which sound originates, such as a chess piece that makes a shuffling noise as it slides to a location on the board. A source emanates sound from a single point in space, or a voluminous area. To produce sound at a point in the scene, create a PHASESource with the engine parameter, for example:let chessPiecePointSource = PHASESource(engine: engine)
Then, add the source to the scene by handing it to the engine. You can add an object as a child to any other object by calling addChild(_:) on the parent. The result models a scene as a connected graph of objects, or an object hierarchy. The following code adds the chess piece as child of the engine’s root:do { try engine.rootObject.addChild(chessPiecePointSource) } 
catch { print ("Failed to add a child object to the scene.") }
PHASE interprets object positions in the coordinate space of the parent, which for the root object is the coordinate space of the scene, or the world space. Set an object’s position by assigning the transform’s first three elements of the last column. The following code sets a chess piece’s position to (0,0,-6), which is 6 meters in front of the world origin (0,0,0):chessPiecePose.columns.3.z -= 6.0
chessPiecePointSource.transform = chessPiecePose
Tip Set the unitsPerMeter parameter to instruct PHASE to interpret transform values in your app’s preferred unit of measurement.Originate sound from a geometric areaFor spatial sounds, the framework requires a 3D position from which the sound originates. To emanate sound from an area larger than a point, for example, the full length of an electric fence in a game, describe the region by configuring a PHASEShape object. The following code models a fence by using a Model I/O plane:let fenceMesh = MDLMesh(
   planeWithExtent: vector3(0.1, 0.1, 0.1), 
   segments: vector2(1, 1), 
   geometryType: .triangles, 
   allocator: nil)

let fenceShape = PHASEShape(engine: engine, mesh: fenceMesh)
let volumetricFenceSource = PHASESource(engine: engine, shapes: [fenceShape])

do { try engine.rootObject.addChild(volumetricFenceSource) } 
catch { print ("Failed to add a child object to the scene.") }
Note You can supply high-resolution geometry to a PHASESource. For collision detection, games usually supply a low-resolution approximation that contains a detailed visual asset to maximize runtime performance. However, PHASEShape supports geometry of any resolution with little performance impact.Create an object that hears soundA PHASEListener is an object within an app that hears sound; it’s the central position and orientation at which the user experiences spatial audio. The framework adjusts the volume of a sound source based on its unique position and orientation with respect to the listener. For example, a sound that plays far off in the distance from the listener plays quietly, and a closer sound plays more loudly. The following code creates a listener and defines its position and orientation in the scene:let origin: simd_float4x4 = matrix_identity_float4x4
let listener = PHASEListener(engine: engine)
listener.transform = origin
Add the listener to the scene by inserting it into the object hierarchy. The following code adds the listener as a child of the engine’s root object:do { try engine.rootObject.addChild(listener) } 
catch { print ("Failed to add child object to the scene.") }
Set up occluder options for obstructed soundThe framework lowers the volume of a sound source when an obstacle blocks its path to the listener. The result creates a realistic effect in cases where, for example, the player takes cover behind a gallery pillar, which reduces the volume of commotion from the other side of the room.To define an obstacle, create a PHASEOccluder with a shape and position that matches the pillar’s visual counterpart. The following code defines an occluder’s geometric shape using Model I/O:defaultOccluderSize: Float = 1.0

let pillarOccluderMesh = MDLMesh.newCylinder(withHeight: 10.0, 
    radii: vector_float2(defaultOccluderSize, defaultOccluderSize), 
    radialSegments: 9, 
    verticalSegments: 1, 
    geometryType: MDLGeometryType.triangles, 
    inwardNormals: false, 
    allocator: nil)
You can tweak the reflectivity of a particular occluder by choosing a physical material that makes up the occluder. The material you choose implements a blend between how much an occluder reflects sound and how much sound passes through it. To select a material, pass its corresponding preset, PHASEMaterialPreset, into a new PHASEMaterial object:let occluderMaterial = PHASEMaterial(engine: engine, preset: .concrete)
let occluderShape = PHASEShape(engine: engine,
   mesh: pillarOccluderMesh,
   materials: [occluderMaterial])

let occluder = PHASEOccluder(engine: engine,
   shapes: [occluderShape])
Position an occluder in the scene by setting its transform. The following code places an occluder midway between the source and listener by dividing the custom defaultSourceDistance variable by two:let defaultSourceDistance: Float = 10.0

var occluderTransform: simd_float4x4 = origin
occluderTransform.columns.3.z -= defaultSourceDistance / 2.0
occluder.transform = occluderTransform
Activate the occluder by adding it into the scene. The following code adds the occluder as a child of the root object:do { try engine.rootObject.addChild(occluder) } 
catch { print ("Failed to add a child object to the scene.") }
Describe the output pipelineAs one of the final stages in audio playback configuration, the app specifies the particular object, or mixer, that combines in-flight audio signals for transmission to the output device. For spatial audio, the app creates a spatial mixer, PHASESpatialMixerDefinition. The following code defines a spatial mixer for two sources:let chessPieceSpatialMixer = PHASESpatialMixerDefinition(
    spatialPipeline: PHASESpatialPipeline(
        flags: .directPathTransmission)!)

let fenceSpatialMixer = PHASESpatialMixerDefinition(
    spatialPipeline: PHASESpatialPipeline(
        flags: .directPathTransmission)!)
The spatial mixer can add environmental layers to the output, such as reflections or reverb, by including the earlyReflections or lateReverb cases, in addition to directPathTransmission, to the flags argument.Adjust volume based on distancePHASE attenuates sound over the distance between a source and a listener by observing the distance model you define on the spatial mixer. As a source emits sound, the spatial mixer adjusts its volume based on the distance from the listener. The farther away the source is from the listener, the more the volume attenuates and the quieter the sound gets with respect to the listener.Important Without a distance model, the spatial mixer plays sound at a constant level, disregarding the distance between the source and the listener.For more information about distance modeling and its various types, geometric and envelope, see Spatial Mixing.PHASEGeometricSpreadingDistanceModelParameters is a model that simulates sound loss over distance realistically. The distance model rolloffFactor emphasizes or deemphasizes this model. At 1.0, sound that emanates between the source and listener loses 6 dB every time distance doubles. At 2.0, the loss doubles. At 0.5, the loss halves, and so on. The following code defines a geometric spatial model for the scene’s spatial mixers:let simpleModel = PHASEGeometricSpreadingDistanceModelParameters()
simpleModel.rolloffFactor = 1.0

chessPieceSpatialMixer.distanceModelParameters = simpleModel
fenceSpatialMixer.distanceModelParameters = simpleModel
Generate a sound eventWhen PHASE understands the layout and configuration of the scene, sound reacts in accordance when your app plays a sound event by using PHASESoundEvent. You generate a sound event from a sound-event node that describes your particular playback needs.First, identify the sound assets for your sound events and register them with the engine’s asset registry. The following code loads two files bundled with the project titled “shuffling.wav” and “buzzing.wav”:let shufflingSoundUrl = Bundle.main.url(forResource: "shuffling", withExtension: "wav")!
var shufflingSoundAsset:PHASESoundAsset!
do {
    shufflingSoundAsset = try engine.assetRegistry.registerSoundAsset(
    url: shufflingSoundUrl,
    identifier: "shufflingSound",
    assetType: PHASEAsset.AssetType.resident,
    channelLayout: nil,
    normalizationMode: .dynamic)
} catch {
    print("Failed to register the sound asset.")
}

let buzzingSoundUrl = Bundle.main.url(forResource: "buzzing", withExtension: "wav")!
var electricBuzzingSoundAsset:PHASESoundAsset!
do {
    electricBuzzingSoundAsset = try engine!.assetRegistry.registerSoundAsset(
    url: buzzingSoundUrl,
    identifier: "buzzingSound",
    assetType: .resident,
    channelLayout: nil,
    normalizationMode: .dynamic)
} catch {
    print("Failed to register the sound asset.")
}
The following code creates sampler nodes for both the shuffling chess piece and electrified fence:// Define the shuffling chess piece one-shot sound.
let shufflingSamplerNode = PHASESamplerNodeDefinition(
    soundAssetIdentifier: shufflingSoundAsset.identifier,
    mixerDefinition: chessPieceSpatialMixer,
    identifier: shufflingSoundAsset.identifier + "_SamplerNode")

shufflingSamplerNode.playbackMode = .oneShot

// Define the buzzing electric fence looping sound.
let electricBuzzingSamplerNode = PHASESamplerNodeDefinition(
    soundAssetIdentifier: electricBuzzingSoundAsset.identifier,
    mixerDefinition: fenceSpatialMixer,
    identifier: electricBuzzingSoundAsset.identifier + "_SamplerNode")

electricBuzzingSamplerNode.playbackMode = .looping
Give PHASE information about the sound-event nodes by registering their assets with the engine:var shufflingSoundEventAsset: PHASESoundEventNodeAsset!
do { shufflingSoundEventAsset = try 
    engine.assetRegistry.registerSoundEventAsset(  
    rootNode: shufflingSamplerNode,
    identifier: shufflingSoundAsset.identifier + "_SoundEventAsset")
} catch { print("Failed to register a sound event asset.") } 

var buzzingSoundEventAsset: PHASESoundEventNodeAsset!
do { buzzingSoundEventAsset = try 
    engine.assetRegistry.registerSoundEventAsset(  
    rootNode: electricBuzzingSamplerNode,
    identifier: electricBuzzingSoundAsset.identifier + "_SoundEventAsset")
} catch { print("Failed to register a sound event asset.") }
Define which sound source plays the audio and the listener that hears it by configuring a PHASEMixerParameters object for each spatial mixer:let chessPieceSpatialMixerParams = PHASEMixerParameters()
chessPieceSpatialMixerParams.addSpatialMixerParameters(
    identifier: chessPieceSpatialMixer.identifier,
    source: chessPiecePointSource,
    listener: listener)

let fenceSpatialMixerParams = PHASEMixerParameters()
fenceSpatialMixerParams.addSpatialMixerParameters(
    identifier: fenceSpatialMixer.identifier,
    source: volumetricFenceSource,
    listener: listener)
To play the sounds, generate a PHASESoundEvent instance for each node and call start(completion:) on the sound event. Associate the source to the sound event by passing its spatialMixerParams through the PHASESoundEvent initializer mixerParameters argument:let buzzingSoundEvent = try! PHASESoundEvent(engine: engine,
    assetIdentifier: buzzingSoundEventAsset.identifier,
    mixerParameters: fenceSpatialMixerParams)

buzzingSoundEvent.start(completion: nil)

let shufflingSoundEvent = try! PHASESoundEvent(engine: engine,
    assetIdentifier: shufflingSoundEventAsset.identifier,
    mixerParameters: chessPieceSpatialMixerParams)

shufflingSoundEvent.start(completion: nil)
Because electricBuzzingSamplerNode and shufflingSamplerNode have no children, both buzzingSoundEventAsset and shufflingSoundEventAsset contain a node hierarchy of only one node. When the app invokes a sound event from these assets, the same audio plays consistently.Tip You can create a more sophisticated node hiearchy that plays different sounds based on your app’s state. By adding multiple nodes that sample varying audio as children to a control node, PHASE plays the right audio for the moment based on control logic that you define. For more information, see Audio Selection and Playback.See AlsoEssentialsPersonalizing spatial audio in your appEnhance the realism of spatial audio output by tracking a person’s head movement and accounting for their personal spatial audio profile.PHASE updatesLearn about important changes to PHASE.

## Sound Event Nodes | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/sound-event-nodes

Collection PHASE  Sound Event Nodes API CollectionSound Event NodesObjects that connect to form a hierarchical tree of audio actions.OverviewTo play sound, your app assembles a hieararchical structure of audio nodes that determine which sound to play at the moment. A tree with two sampler nodes branching from a switch node plays only one sampler, depending on your app’s state. You set the control logic in advance that specifies the conditions upon which the switch node toggles. To play the same audio consistently, create a tree with a single sampler node.To invoke the tree, create a sound event that references the tree and call start(completion:) on the sound event.TopicsAudio-Providing Nodesclass PHASESamplerNodeDefinitionA node that plays complete audio data.enum PHASEPlaybackModeLoop options for audio playback.class PHASEPushStreamNodeDefinitionA node that plays a sequence of audio buffers.class PHASEPushStreamNodeAn audio stream you manage to provide a sound buffer data.struct PHASEPushStreamBufferOptionsOptions that inform PHASE of an audio-stream buffer’s playback priority.enum PHASECalibrationModeCalibration options for sound pressure level.class PHASEGeneratorNodeDefinitionA base class for nodes that provide audio data to generate sound.Control Nodesclass PHASESwitchNodeDefinitionA node that passes invocation to only one of its child nodes.class PHASERandomNodeDefinitionA sound event node that invokes one of its child nodes at random.class PHASEBlendNodeDefinitionA node that smoothly fades between the audio of its child nodes.class PHASEContainerNodeDefinitionA node that plays all its children at the same time.See AlsoAudio Selection and Playbackclass PHASESoundAssetA sound resource stored in the asset registry.class PHASESoundEventAn object that determines which audio to play.enum RenderingStateThe playback status of audio.class PHASESoundEventNodeDefinitionA base class for sound event nodes that connect to form a node hierarchy.class PHASESoundEventNodeAssetA template object for sounds that can play in reaction to environmental state.class PHASEAssetA base class that adds a name to framework assets.

## Spatial Mixing | Apple Developer Documentation
*Source:* https://developer.apple.com/documentation/phase/spatial-mixing

Collection PHASE  Spatial Mixing API CollectionSpatial MixingDefine environmental characteristics that determine how sound plays in your app’s 3D soundscape.OverviewSpatial mixing refers to the process by which PHASE emits one or more simultaneous sounds in 3D space and layers in optional environmental effects. For a walkthrough that demonstrates spatial mixing, see Playing sound from a location in a 3D scene.TopicsSetupclass PHASESpatialMixerDefinitionAn audio-layering object that produces environmental effects and plays sound with a 3D position and orientation.Sound Reflections and Resonanceclass PHASESpatialPipelineAn object that specifies the volume of optional environmental effects.class PHASESpatialPipelineEntryAn audio layer with an adjustable volume for a spatial mixer’s output.struct PHASESpatialCategorySound resonance effects for spatial mixing.struct FlagsSound resonance options for a spatial pipeline.Distance Modelingclass PHASEGeometricSpreadingDistanceModelParametersAn object that dissipates sound frequencies over distance.class PHASEEnvelopeDistanceModelParametersA graph of points and curves that shapes the volume of a sound over distance.class PHASEDistanceModelFadeOutParametersA distance over which the framework fades out sound.class PHASEDistanceModelParametersA base class for a sound’s rate of change over distance.Sound Directivityclass PHASECardioidDirectivityModelParametersAn object that directs sound in a heart-shaped curve surrounding a sound source.class PHASECardioidDirectivityModelSubbandParametersA data set that projects sound of a certain frequency outward in the shape of a heart.class PHASEConeDirectivityModelParametersAn object that directs sound in a cone-shaped curve that extends from a sound source.class PHASEConeDirectivityModelSubbandParametersA data set that projects sound of a certain frequency outward in the shape of a cone.class PHASEDirectivityModelParametersA base class for objects that direct sound.See AlsoAudio Layering and Effectsclass PHASEChannelMixerDefinitionAn audio-layering object that routes sound directly to the device’s output.class PHASEAmbientMixerDefinitionAn audio-layering object that outputs sound in a particular direction in 3D space.class PHASEMixerDefinitionAn object to initialize a mixer with a given configuration.class PHASEMixerAn object that combines multiple audio signals into a single signal.class PHASEDefinitionA base class that adds a name to framework definitions.
